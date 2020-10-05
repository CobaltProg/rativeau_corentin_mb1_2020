FROM mhart/alpine-node:3.12.0
WORKDIR /app
COPY ./package.json ./
RUN npm install
EXPOSE 2368
CMD ["npm","start"]
