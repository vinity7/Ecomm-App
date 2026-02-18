# Builder stage: install dependencies and build
FROM node:18-alpine AS builder

# Set up the work directory
WORKDIR /app

# Copy package manifests and install deps
COPY package*.json ./
RUN npm install

# Copy source and build
COPY . .
RUN npm run build

# Development runtime (optional)
FROM node:alpine AS development
WORKDIR /app
COPY --from=builder /app .
CMD ["npm","run","dev"]

# Production runtime using nginx
FROM nginx:alpine AS production

COPY --from=builder /app/dist /usr/share/nginx/html

EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
