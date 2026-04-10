# -- Shared Base -- 
FROM node:20-alpine AS base   
WORKDIR /app
COPY package*.json ./
RUN npm install

COPY . .
    
# -- Dev Stage --
FROM base AS dev


CMD [ "npm", "run", "dev" ]

# ---- Build Stage ----
FROM base AS build

  
RUN npm run build


# ---- Production Stage ----
FROM nginx:alpine

COPY --from=build /app/dist /usr/share/nginx/html

COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD [ "nginx", "-g", "daemon off;" ]