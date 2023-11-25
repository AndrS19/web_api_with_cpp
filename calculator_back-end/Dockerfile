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

# Завантажте librestbed-dev та librestbed0
RUN wget http://mirrors.kernel.org/ubuntu/pool/universe/r/restbed/librestbed-dev_4.0~dfsg1-5build2_amd64.deb \
    && wget http://mirrors.kernel.org/ubuntu/pool/universe/r/restbed/librestbed0_4.0~dfsg1-5build2_amd64.deb

# Встановіть завантажені пакети
RUN dpkg -i librestbed-dev_4.0~dfsg1-5build2_amd64.deb \
    && dpkg -i librestbed0_4.0~dfsg1-5build2_amd64.deb

# Встановіть будь-які відсутні залежності
RUN apt-get install -f

# Виконуються необхідні кроки для збірки проекту
RUN cmake -H. -Bbuild && cmake --build build --config Release --target all

# Команда, яка виконається при старті контейнера
CMD ["./build/CalculatorAPI"]
