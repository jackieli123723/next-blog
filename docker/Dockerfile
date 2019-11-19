#FROM registry.docker-cn.com/library/node:9.5-alpine
FROM node:latest
MAINTAINER jackeili
WORKDIR /app
COPY . /app
RUN npm install --global pm2
RUN npm install 
# Build app
#RUN npm run build:content
RUN npm run build

# Expose the listening port
EXPOSE 13090

# Launch app with PM2
#CMD [ "pm2-runtime", "start", "npm", "--", "start" ]
CMD ["npm","run","start:prod"]
