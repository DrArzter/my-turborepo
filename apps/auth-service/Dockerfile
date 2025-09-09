FROM node:18 AS builder

WORKDIR /app

RUN npm install -g pnpm

COPY package.json pnpm-lock.yaml pnpm-workspace.yaml ./
COPY apps/auth-service/package.json ./apps/auth-service/
COPY packages/database/package.json ./packages/database/

RUN pnpm install --frozen-lockfile

COPY . .

RUN pnpm --filter auth-service build

RUN pnpm --filter auth-service deploy --legacy --prod /prod/auth-service

FROM node:18-alpine

WORKDIR /app

RUN addgroup --system --gid 1001 nodejs
RUN adduser --system --uid 1001 nodejs
USER nodejs

COPY --from=builder --chown=nodejs:nodejs /prod/auth-service .

# Запускаем приложение
CMD ["node", "dist/main.js"]