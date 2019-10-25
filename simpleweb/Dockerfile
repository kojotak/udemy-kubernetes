# base image
FROM node:alpine

WORKDIR /usr/app

# install dependencies
# copy packages first, so that they will be cached as docker layer
COPY ./package.json ./
RUN npm install
COPY ./ ./

# default command
CMD ["npm", "start"]