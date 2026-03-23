# Stage 1: Base
FROM node:20-alpine AS base
WORKDIR /app
COPY package*.json ./

# Stage 2: Development
FROM base AS development
RUN npm install
COPY . .
ENV NODE_ENV=development
EXPOSE 8080
CMD ["npm", "run", "dev"]

# Stage 3: Build for production
FROM base AS build
RUN npm install
COPY . .
RUN npm run build

# Stage 4: Production Runtime (Nginx)
FROM nginx:stable-alpine AS production
# Copy build output from Stage 3
COPY --from=build /app/dist /usr/share/nginx/html
# Copy custom nginx config
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
