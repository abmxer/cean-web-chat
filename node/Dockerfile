FROM node:5.6.0

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

COPY package.json package.json

RUN npm install
RUN npm install -g nodemon

CMD [ "nodemon", "app.js" ]

EXPOSE 3010
