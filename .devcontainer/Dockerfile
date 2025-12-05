FROM node:24

WORKDIR /mobimart/app

COPY package*.json ./
RUN npm install

COPY . .

ENTRYPOINT npm start

