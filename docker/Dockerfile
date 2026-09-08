FROM python:3.12-alpine

RUN apk --update --no-cache --no-progress add git alpine-sdk libffi-dev openssl autoconf automake libtool

RUN adduser -u 1600 -D service-0net

USER service-0net:service-0net

WORKDIR /home/service-0net

COPY . .

RUN python3 -m pip install --r requirements.txt

# the part below is updated with source updates

COPY . .

ENTRYPOINT python3 zeronet.py --ui-ip "*" --fileserver-port 26552 \
    --tor $TOR_ENABLED --tor-controller tor:$TOR_CONTROL_PORT \
    --tor-proxy tor:$TOR_SOCKS_PORT --tor-password $TOR_CONTROL_PASSWD

CMD main

EXPOSE 43110 26552
