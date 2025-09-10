FROM node:18 AS builder

WORKDIR /app

RUN npm install -g pnpm

COPY package.json pnpm-lock.yaml pnpm-workspace.yaml ./
COPY apps/web/package.json ./apps/web/

COPY packages/database/package.json ./packages/database/

RUN pnpm install --frozen-lockfile

COPY . .

RUN pnpm --filter web build

RUN pnpm --filter web deploy --legacy --prod /prod/web

FROM node:18-alpine

WORKDIR /app

RUN addgroup --system --gid 1001 nodejs
RUN adduser --system --uid 1001 nodejs
USER nodejs

COPY --from=builder --chown=nodejs:nodejs /prod/web .

CMD ["node_modules/.bin/next", "start"]