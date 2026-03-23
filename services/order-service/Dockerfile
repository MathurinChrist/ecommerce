FROM node:20-alpine AS base
WORKDIR /app
COPY package*.json ./

FROM base AS development
RUN npm install
COPY . .
ENV NODE_ENV=development
EXPOSE 3002
CMD ["npm", "run", "dev"]

FROM base AS build
RUN npm install --only=production
COPY . .

FROM node:20-alpine AS production
WORKDIR /app
ENV NODE_ENV=production


RUN addgroup -S mathurinGroup && adduser -S mathurin -G mathurinGroup

COPY --from=build /app/node_modules ./node_modules
COPY --from=build /app/src ./src
COPY --from=build /app/package*.json ./

USER mathurin

EXPOSE 3002

CMD ["node", "src/app.js"]
