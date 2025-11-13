# client/Dockerfile
FROM node:18 AS builder
WORKDIR /app
COPY client/package*.json ./client/
# If the repo's client package.json sits in client/ (adjust if paths differ)
RUN cd client && npm install
COPY client/ ./client
RUN cd client && npm run build

# serve with nginx
FROM nginx:alpine
COPY --from=builder /app/client/build /usr/share/nginx/html
# remove default nginx conf and use a simple one that forwards API calls
RUN rm /etc/nginx/conf.d/default.conf
COPY client/nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
