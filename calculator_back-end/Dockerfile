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

# Встановлення restbed
RUN git clone https://github.com/Corvusoft/restbed.git \
    && cd restbed \
    && git checkout $(git describe --tags `git rev-list --tags --max-count=1`) \
    && mkdir build \
    && cd build \
    && cmake -DBUILD_SSL=NO -DBUILD_TESTS=NO -DASIO_INCLUDE_DIR=/usr/include .. \
    && make install \
    && cd ../..

# Виконуються необхідні кроки для збірки проекту
RUN cmake -H. -Bbuild && cmake --build build --config Release --target all

# Команда, яка виконається при старті контейнера
CMD ["./build/CalculatorAPI"]
