# # build stage
# FROM node:14.15-alpine 
# #lts-alpine as build-stage 이 안되어서 위와 같이 실행함
# ENV NODE_ENV=dev
# WORKDIR /app
# RUN apk update && apk upgrade && apk add --no-cache bash git openssh
# RUN npm install --production
# COPY . .
# # RUN npm ci && npm run serve && npm run build
# # 위에 안되면 npm i @vue/cli-service && npm run build
# RUN npm i @vue/cli-service && npm run build
# EXPOSE 8080
# CMD ["npm", "start"]

# # # production stage
# # FROM nginx:stable-alpine as production-stage
# # COPY --from=build-stage /app/dist /usr/share/nginx/html
# # EXPOSE 8080
# # CMD ["nginx", "-g", "daemon off;"]



######################################3

FROM node:lts-alpine as build-stage
WORKDIR /app
COPY package*.json ./
RUN npm install --production --silent && mv node_modules ../
COPY . .
RUN npm install -g @vue/cli-service
RUN npm install @vue/cli-plugin-babel
RUN npm run build
# EXPOSE 8090
EXPOSE 80 8090
CMD ["npm", "start"]

FROM nginx:stable-alpine as production-stage
COPY --from=build-stage /app/dist /usr/share/nginx/html
# EXPOSE 8080
EXPOSE 80 8090
CMD ["nginx", "-g", "daemon off;"]