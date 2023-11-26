# Етап 1: Використовуємо офіційний образ Node.js для збірки фронтенду
FROM node:latest AS builder

# Встановлюємо робочу директорію в контейнері
WORKDIR /app

# Копіюємо файли package.json та package-lock.json (якщо вони є) в контейнер
COPY package*.json ./

# Встановлюємо залежності
RUN npm install

# Копіюємо вміст поточної директорії (де знаходиться Dockerfile) в контейнер
COPY . .

# Запускаємо команду для збірки проекту
RUN npm run build

# Етап 2: Використовуємо офіційний образ Nginx для обслуговування збірки проекту
FROM nginx:latest

# Видалення стандартної сторінки Nginx
RUN rm -rf /usr/share/nginx/html/*

# Копіюємо артефакт (dist) у каталог Nginx
COPY --from=builder /app/build /usr/share/nginx/html/

# Видаляємо попередню конфігурацію Nginx що стоїть по замовчуванню
RUN rm -f /etc/nginx/http.d/default.conf

# Завантажуємо власну конфігурацію Nginx в образ
COPY ./nginx.conf /etc/nginx/http.d/

# Вказуємо порт, на якому буде слухати Nginx (за потреби змініть на свій порт)
EXPOSE 80

# Запускаємо Nginx у фоновому режимі при запуску контейнера
CMD ["nginx", "-g", "daemon off;"]
