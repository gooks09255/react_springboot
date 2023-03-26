# build environment
FROM node:16.13.1-alpine as build
RUN apk add git

WORKDIR /app
ENV PATH ./node_modules/.bin:$PATH
COPY package*.json /app/
RUN npm install --legacy-peer-deps
COPY . /app/
RUN GENERATE_SOURCEMAP=false npm run build

EXPOSE 80

CMD ["npm", "start"]
