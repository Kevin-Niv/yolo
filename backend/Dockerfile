#For Building

ARG NODE_VERSION=19.0.0-alpine

FROM node:${NODE_VERSION} AS builder

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install --production

COPY . .

#For running Inside the container 

FROM node:${NODE_VERSION} AS runner

WORKDIR /usr/src/app

COPY --from=builder /usr/src/app /usr/src/app

EXPOSE 5000

CMD ["npm", "start"]