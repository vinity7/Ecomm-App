# Node version-package we are using to build the application
FROM   node:18-alpine 

# Set up the work directory
WORKDIR/app

# Copy the package files
COPY package*.json ./


# run the install command
COPY . .



# copy the entire code base
RUN npm run build 


# run the build command
FROM node:alpine AS development


# something different  
FROM nginx:alpine AS production

COPY --from=builder /app/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
