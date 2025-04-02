# Stage 0: Build stage
FROM node:18-alpine AS build-stage

WORKDIR /app

COPY package*.json /app/
RUN npm install

COPY ./ /app/

ARG configuration=production
RUN npm run build -- --configuration $configuration

# Stage 1: Production stage with Nginx
FROM nginx:1.25-alpine

# Copia específicamente los archivos de la carpeta browser
COPY --from=build-stage /app/dist/my-angular-project/browser/ /usr/share/nginx/html/

# Copy custom Nginx config
COPY ./nginx.conf /etc/nginx/conf.d/default.conf
