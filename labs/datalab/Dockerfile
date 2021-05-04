FROM debian:buster

RUN apt update -y
RUN apt install -y build-essential make gcc gcc-multilib
COPY run_tests.sh /run_tests.sh

ENTRYPOINT ["/run_tests.sh"]
