FROM debian:testing

RUN apt-get update -y
RUN apt-get install -y eatmydata
RUN eatmydata apt-get install -y \
                                info \
                                gcc \
                                gcc-doc \
                                gdb \
                                gdb-doc \
                                qemu-user-static \
                                gcc-multilib-sparc64-linux-gnu
