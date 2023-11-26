# Використовуємо офіційний образ Alpine Linux
FROM alpine:latest

# Оновлення індексу пакетів і встановлення Nginx
RUN apk update && apk add nginx

# Видалення стандартної сторінки Nginx
RUN rm -rf /usr/share/nginx/html/*

# Виконає необхідні кроки для збірки та запуску front-end проекту
RUN npm install && npm run build

# Копіюємо артефакт (dist) у каталог Nginx
COPY ./build /usr/share/nginx/html/

# Видаляємо попередню конфігурацію Nginx що стоїть по замовчуванню
RUN rm -f /etc/nginx/http.d/default.conf

# Завантажуємо власну конфігурацію Nginx в образ
COPY ./nginx.conf /etc/nginx/http.d/

# Відкриваємо порт 80 для HTTP
EXPOSE 80

# Запускаємо Nginx у фоновому режимі при запуску контейнера
CMD ["nginx", "-g", "daemon off;"]
