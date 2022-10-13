# Stage 1: Build an Angular Docker Image
FROM docker.io/node as build
WORKDIR /app
COPY package*.json /app/
RUN npm install
COPY . /app
ARG configuration=production
RUN npm run build -- --outputPath=./dist/out --configuration $configuration
# Stage 2, use the compiled app, ready for production with Nginx
FROM docker.io/bitnami/nginx
COPY --from=build /app/dist/out/ /app
COPY /nginx-custom.conf /opt/bitnami/nginx/conf/nginx.conf:ro
