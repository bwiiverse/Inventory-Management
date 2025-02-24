# Use Node.js 22 to build the Angular app
FROM node:22 AS build

# Set the working directory inside the container
WORKDIR /app

# Copy package files and install dependencies
COPY package.json package-lock.json ./
RUN npm install  # 🔥 This ensures dependencies are installed inside the container

# Copy the entire Angular project into the container
COPY . .

# Build the Angular app
RUN npm run build -- --configuration=production  # 🔥 Ensure the app is built

# Use Nginx to serve the built Angular app
FROM nginx:alpine

# Copy the built app from the previous stage to Nginx’s HTML directory
COPY --from=build /app/dist/frontend/browser /usr/share/nginx/html

# Expose port 80 so the Angular app can be accessed from outside the container
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
