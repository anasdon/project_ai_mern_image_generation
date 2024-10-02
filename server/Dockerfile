FROM alpine:3.19
RUN npm install -g nodemon
WORKDIR /app
COPY package.json .
COPY . .
EXPOSE 300
CMD ["npm", "run", "dev"]
