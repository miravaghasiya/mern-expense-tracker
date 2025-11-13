# server/Dockerfile
FROM node:18
WORKDIR /usr/src/app
# copy package.json first to leverage layer caching
COPY server/package*.json ./
RUN npm install --production
COPY server/ .
# If server expects env var PORT or MONGO_URI, we'll use defaults
ENV PORT=5000
EXPOSE 5000
CMD ["npm", "start"]

