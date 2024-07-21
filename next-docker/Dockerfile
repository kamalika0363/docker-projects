# Stage 1: Build
FROM node:20-alpine AS builder
WORKDIR /usr/src/app
RUN npm install -g pnpm
COPY package*.json ./
ENV NEXT_TELEMETRY_DISABLED 1
RUN pnpm install 
COPY . .
RUN pnpm run build


# Stage 2: Serve
FROM node:20-alpine
WORKDIR /usr/src/app
RUN npm install -g pnpm

COPY --from=builder /usr/src/app/package*.json ./
COPY --from=builder /usr/src/app/.next .next/
COPY --from=builder /usr/src/app/public public/
COPY --from=builder /usr/src/app/node_modules node_modules/

RUN pnpm install next
CMD ["pnpm", "start"]