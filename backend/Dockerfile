ARG NODE_VERSION=19.0.0-alpine

FROM node:${NODE_VERSION} as builder

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install --production

COPY . .

FROM node:${NODE_VERSION} as runner

WORKDIR /usr/src/app

COPY --from=builder /usr/src/app /usr/src/app

EXPOSE 5000

CMD ["npm", "start"]