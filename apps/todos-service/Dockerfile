FROM node:18 AS builder

WORKDIR /app

RUN npm install -g pnpm

COPY package.json pnpm-lock.yaml pnpm-workspace.yaml ./
COPY apps/todos-service/package.json ./apps/todos-service/
COPY packages/database/package.json ./packages/database/

RUN pnpm install --frozen-lockfile

COPY . .

RUN pnpm --filter todos-service build

RUN pnpm --filter todos-service deploy --legacy --prod /prod/todos-service

FROM node:18-alpine

WORKDIR /app

RUN addgroup --system --gid 1001 nodejs
RUN adduser --system --uid 1001 nodejs
USER nodejs

COPY --from=builder --chown=nodejs:nodejs /prod/todos-service .

CMD ["node", "dist/main.js"]