# syntax=docker/dockerfile:1.4

FROM node:18 AS deps
WORKDIR /app

COPY package*.json ./
RUN --mount=type=cache,target=/root/.npm \
    npm ci --only=production

FROM node:18-slim AS runner
WORKDIR /app

COPY --from=deps /app/node_modules ./node_modules
COPY --from=deps /app/package*.json ./

# Copy gateway source
COPY . .

ENV NODE_ENV=production
EXPOSE 5921

# Gateway entrypoint – in your logs, src/gateway.js DID NOT exist,
# so src/index.js is likely correct. If your real file is src/gateway.js,
# change the next line to: ["node","src/gateway.js"]
CMD ["node", "src/index.js"]
