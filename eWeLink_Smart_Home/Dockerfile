# ARG BUILD_FROM
# FROM ${BUILD_FROM}
FROM node:25-alpine

ENV LANG=C.UTF-8
ENV CK_API_ENV=prod
# Added
ENV HA_URL=http://192.168.5.34:8123
ENV SUPERVISOR_TOKEN=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiIzZTMwODM1Zjg0OGM0NGE2OGU4NDdhMWIwOWFiM2E1MCIsImlhdCI6MTc3MDI2MjY2NywiZXhwIjoyMDg1NjIyNjY3fQ.bp7Mv0fNXurE3WMPcbTYk7I_Bc8-SjAGxU7krUwToEQ

RUN apk add --no-cache \
    nodejs \
    npm \
    python3 \
    build-base

WORKDIR /workspace
RUN mkdir -p /workspace/node_modules

COPY ["./dist", "./package.json", "/workspace/"]
RUN npm install --production --save-exact
COPY ["./node_modules", "/workspace/node_modules/"]

COPY docker-entrypoint.sh /usr/local/bin/
RUN chmod +x /usr/local/bin/docker-entrypoint.sh

ENTRYPOINT ["/usr/local/bin/docker-entrypoint.sh"]
EXPOSE 3000
CMD ["npm", "start"]