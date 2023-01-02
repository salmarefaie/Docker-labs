FROM node:alpine3.16 AS build

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

RUN npm run build

# Deploment "nginx"
FROM  nginx:alpine

COPY --from=build /app/build /usr/share/nginx/html

EXPOSE 80

CMD [ "nginx", "-g", "daemon off;" ]

#sudo docker build -t my-app2:1.0 .
# sudo docker run -it --name multi -p 8001:80  my-app2:1.0