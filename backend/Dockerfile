### STAGE-1 ###

FROM node:24-alpine AS builder 
WORKDIR /app
COPY package*.json ./
RUN npm ci --omit=dev


#### STAGE-2 ###

FROM node:24-alpine 
WORKDIR /app
RUN addgroup -S nodegroup && adduser -S nodeuser -G nodegroup
USER nodeuser
COPY --from=builder /app/node_modules ./node_modules
COPY package*.json ./
COPY src ./src
EXPOSE 5000
HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \
    CMD node -e "require('http').get('http://localhost:5000/healthz', r => process.exit(r.statusCode === 200 ? 0 : 1)).on ('error', () => process.exit(1))"
CMD ["node", "src/server.js"]






