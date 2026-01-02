FROM node:20-alpine AS builder

WORKDIR /app

COPY package*.json ./

RUN npm ci --only=production

FROM node:20-alpine

WORKDIR /app

RUN addgroup -g 1001 -S nodejs && \
    adduser -S nodejs -u 1001 && \
    apk add --no-cache wget

COPY --from=builder /app/node_modules ./node_modules
COPY --chown=nodejs:nodejs src ./src
COPY --chown=nodejs:nodejs package.json ./

USER nodejs

EXPOSE 3000

CMD ["node", "src/index.js"]
