FROM node:13.6.0-alpine

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

COPY package*.json ./
RUN rm -rf package-lock.json node_modules
RUN npm install

COPY . /usr/src/app

USER node
CMD [ "npm", "start" ]
