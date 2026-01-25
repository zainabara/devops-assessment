# -------------------------
# 1. Builder Stage
# -------------------------
FROM node:20-alpine AS builder

WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build

# -------------------------
# 2. Production Stage
# -------------------------
FROM node:20-alpine

WORKDIR /app

# Install serve as root
RUN npm install -g serve

# Create non-root user
RUN adduser -D devuser
USER devuser

# Copy built files
COPY --from=builder /app/dist ./dist

EXPOSE 5173
CMD ["serve", "-s", "dist", "-l", "5173"]

