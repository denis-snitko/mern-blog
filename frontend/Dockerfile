FROM node:16-alpine3.14 as build

WORKDIR /app

COPY package*.json ./

RUN npm install

# RUN npm ci --silent
# RUN npm install react-scripts@3.4.1 -g --silent

COPY . ./

RUN npm run build

FROM nginx:stable-alpine

WORKDIR /app

COPY --from=build /app/build/ /usr/share/nginx/html

RUN rm /etc/nginx/conf.d/default.conf

COPY nginx/nginx.conf /etc/nginx/conf.d

CMD ["nginx", "-g", "daemon off;"]