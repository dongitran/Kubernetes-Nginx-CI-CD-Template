FROM node:latest

WORKDIR /usr/src/app

COPY nodejs/package*.json ./

RUN npm install

COPY . .

EXPOSE 3000

CMD [ "node", "server.js" ]
