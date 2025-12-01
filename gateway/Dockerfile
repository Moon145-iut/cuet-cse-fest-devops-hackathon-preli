# syntax=docker/dockerfile:1.4

FROM node:18 AS deps
WORKDIR /app
COPY package*.json ./

RUN --mount=type=cache,target=/root/.npm \
    npm ci --only=production

FROM node:18-slim AS runner
WORKDIR /app

COPY --from=deps /app /app
COPY . .

EXPOSE 5921
CMD ["node", "src/index.js"]
