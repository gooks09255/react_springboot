# build environment
FROM node:16.13.1-alpine as build
RUN apk add git

WORKDIR /app
ENV PATH ./node_modules/.bin:$PATH
COPY package*.json /app/
RUN npm install --legacy-peer-deps
COPY . /app/
RUN GENERATE_SOURCEMAP=false npm run build

# production environment
FROM nginx:stable-alpine
COPY --from=build /app/build /usr/share/nginx/html
RUN rm /etc/nginx/conf.d/default.conf
COPY ./nginx.conf /etc/nginx/conf.d

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
