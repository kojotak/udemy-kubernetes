# main dockerfile for frontend app and nginx

FROM node:alpine as builder
WORKDIR '/app'
COPY package.json .
RUN npm install
COPY . .
RUN npm run builder

FROM nginx

# expose port for AWS
EXPOSE 80

# use files from previous app
COPY --from=builder /app/build /usr/share/nginx/html
#nginx image already has command for starting nginx, so no need for RUN here...