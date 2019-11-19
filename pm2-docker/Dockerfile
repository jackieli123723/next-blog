FROM keymetrics/pm2:latest-alpine
MAINTAINER jackeili
WORKDIR /app
COPY . /app

RUN npm install 
RUN npm run build

# Expose the listening port
EXPOSE 13091

# Show current folder structure in logs
RUN ls -al -R

CMD [ "pm2-runtime", "start", "ecosystem.config.js" ]