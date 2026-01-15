FROM node:20-alpine
ENV PNPM_HOME="/pnpm"
ENV PATH="$PNPM_HOME:$PATH"
RUN corepack enable

# Installing libvips-dev for sharp Compatibility
RUN apk update && apk add --no-cache build-base gcc autoconf automake zlib-dev libpng-dev nasm bash vips-dev git

WORKDIR /app
# Copy root config
COPY package.json pnpm-lock.yaml pnpm-workspace.yaml ./
# Copy cms config
COPY apps/cms/package.json ./apps/cms/package.json

RUN pnpm install --frozen-lockfile

COPY . .

WORKDIR /app/apps/cms
RUN pnpm build

EXPOSE 1337
CMD ["pnpm", "start"]
