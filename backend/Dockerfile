# syntax=docker/dockerfile:1.4

FROM node:18 AS deps
WORKDIR /app

# Efficient dependency install with cache
COPY package*.json ./
RUN --mount=type=cache,target=/root/.npm \
    npm ci --only=production

FROM node:18-slim AS runner
WORKDIR /app

# Copy built deps and code
COPY --from=deps /app /app
COPY . .

EXPOSE 3847
CMD ["node", "src/index.js"]
