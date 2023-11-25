# Використовує офіційний образ C++ від Docker Hub
FROM gcc:latest

# Встановлює робочу директорію в контейнері
WORKDIR /usr/src/app

# Копіює вміст поточної директорії (де знаходиться Dockerfile) в контейнер
COPY . .

# Встановлює CMake
RUN apt-get update && \
    apt-get install -y cmake

# Встановлення ASIO
RUN apt-get update && apt-get install -y libasio-dev

# Встановлення бібліотеки restbed
RUN apt-get update && apt-get install -y librestbed-dev

# Виконуються необхідні кроки для збірки проекту
RUN cmake -H. -Bbuild && cmake --build build --config Release --target all

# Команда, яка виконається при старті контейнера
CMD ["./build/CalculatorAPI"]
