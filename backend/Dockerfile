# syntax=docker/dockerfile:1.4

# 1. Install dependencies
FROM node:18 AS deps
WORKDIR /app

# Copy package.json and package-lock.json if available
COPY package*.json ./

# Install only production dependencies
RUN npm install --production

# 2. Build the runtime image
FROM node:18-slim AS runner
WORKDIR /app

# Copy installed dependencies
COPY --from=deps /app/node_modules ./node_modules

# Copy application code
COPY . .

# Expose the port your app listens on
EXPOSE 3847

# Start the application
CMD ["node", "src/index.js"]
