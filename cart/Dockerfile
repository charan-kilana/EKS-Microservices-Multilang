FROM node:14

ENV INSTANA_AUTO_PROFILE true

EXPOSE 8080

WORKDIR /opt/server

COPY * /opt/server/

RUN npm install


CMD ["node", "server.js"]

