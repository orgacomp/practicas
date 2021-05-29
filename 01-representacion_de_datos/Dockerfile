FROM debian:testing

RUN echo "deb http://deb.debian.org/debian buster-backports main contrib non-free" >> /etc/apt/sources.list.d/buster-backports.list && \
    echo "deb http://deb.debian.org/debian buster non-free" >> /etc/apt/sources.list && \
    apt-get update -y && apt-get install -y eatmydata
RUN eatmydata apt-get install -y \
                                info \
                                gcc \
                                gcc-doc \
                                gdb \
                                gdb-doc \
                                qemu-user-static \
                                gcc-multilib-sparc64-linux-gnu
