FROM node:24-alpine AS build

WORKDIR /app

COPY package.json package-lock.json ./
RUN npm ci

COPY . .

RUN npm run build -- --configuration production

FROM nginxinc/nginx-unprivileged:alpine

COPY --from=build /app/dist/book-front/browser /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]