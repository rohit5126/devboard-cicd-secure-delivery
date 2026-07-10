# Pin a specific Node version (never a floating `latest`).
FROM node:20-alpine AS prod

WORKDIR /app


# Copy the source and build the production bundle into /dist.
COPY package*.json ./

RUN npm ci

COPY . .
RUN npm run build

#stage 2 for multi stage build

FROM node:20-alpine

WORKDIR /app

RUN npm install -g vite@5 && npm cache clean --force

COPY --from=prod /app/dist ./dist

COPY vite.preview.config.js ./vite.config.js

RUN addgroup -S app && adduser -S -G app app
RUN chown -R app:app /app
USER app

# Vite preview serves the built bundle on this port.
EXPOSE 4173

# 0.0.0.0 so the server is reachable from outside the container.
CMD ["vite", "preview", "--host", "0.0.0.0", "--port", "4173"]
