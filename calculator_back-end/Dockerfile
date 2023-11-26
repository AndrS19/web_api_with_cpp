# Використовує офіційний образ C++ від Docker Hub
FROM gcc:latest

# Встановлює робочу директорію в контейнері
WORKDIR /usr/src/app

# Копіює вміст поточної директорії (де знаходиться Dockerfile) в контейнер
COPY . .

# Встановлює CMake та ASIO
RUN apt-get update && \
    apt-get install -y cmake libasio-dev

# Завантажте librestbed-dev, librestbed0 та libssl1.1
RUN wget http://mirrors.kernel.org/ubuntu/pool/universe/r/restbed/librestbed-dev_4.0~dfsg1-5build2_amd64.deb \
    && wget http://mirrors.kernel.org/ubuntu/pool/universe/r/restbed/librestbed0_4.0~dfsg1-5build2_amd64.deb \
    && wget http://archive.ubuntu.com/ubuntu/pool/main/o/openssl/libssl1.1_1.1.0g-2ubuntu4_amd64.deb

# Встановіть завантажені пакети та їх залежності
RUN dpkg -i libssl1.1_1.1.0g-2ubuntu4_amd64.deb && \
    dpkg -i librestbed0_4.0~dfsg1-5build2_amd64.deb && \
    dpkg -i librestbed-dev_4.0~dfsg1-5build2_amd64.deb && \
    apt-get install -f

# Виконуються необхідні кроки для збірки проекту
RUN cmake -H. -Bbuild && cmake --build build --config Release --target all

EXPOSE 8000

# Команда, яка виконається при старті контейнера
CMD ["./build/CalculatorAPI"]
