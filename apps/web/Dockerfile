# --- Этап 1: Сборка и подготовка к развертыванию (Builder) ---
FROM node:18 AS builder

WORKDIR /app

RUN npm install -g pnpm

# Копируем все package.json и lock-файлы для полной установки
COPY package.json pnpm-lock.yaml pnpm-workspace.yaml ./
COPY apps/auth-service/package.json ./apps/auth-service/
COPY apps/todos-service/package.json ./apps/todos-service/
COPY packages/database/package.json ./packages/database/
COPY apps/web/package.json ./apps/web/

# Устанавливаем ВСЕ зависимости для всего monorepo
RUN pnpm install --frozen-lockfile

# Копируем весь исходный код
COPY . .

# Собираем ТОЛЬКО web
RUN pnpm --filter web build

# Создаем чистую папку для развертывания ТОЛЬКО с production-зависимостями
RUN pnpm --filter web deploy --legacy --prod /prod/web


# --- Этап 2: Финальный, чистый образ (Production) ---
FROM node:18-alpine

WORKDIR /app

# Создаем пользователя
RUN addgroup --system --gid 1001 nodejs
RUN adduser --system --uid 1001 nodejs
USER nodejs

# Копируем ВСЁ готовое для запуска из папки /prod/web
COPY --from=builder --chown=nodejs:nodejs /prod/web .

# Команда для запуска Next.js приложения
CMD ["node_modules/.bin/next", "start"]