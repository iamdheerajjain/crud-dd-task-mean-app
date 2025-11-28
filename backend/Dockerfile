FROM node:18

WORKDIR /app

COPY package*.json ./

RUN npm install -g npm@latest && npm install

COPY . .

EXPOSE 8080

CMD ["node", "server.js"]