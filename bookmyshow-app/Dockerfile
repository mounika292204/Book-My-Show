# -------------------------
# Stage 1: Build React App
# -------------------------
FROM node:18 AS build

WORKDIR /app

# Copy dependency files
COPY package.json package-lock.json ./

# Install dependencies
RUN npm install --legacy-peer-deps

# Copy project files
COPY . .

# Build production files
RUN npm run build


# -------------------------
# Stage 2: Serve with Nginx
# -------------------------
FROM nginx:alpine

# Remove default nginx static files
RUN rm -rf /usr/share/nginx/html/*

# Copy build output from previous stage
COPY --from=build /app/build /usr/share/nginx/html

# Expose port 80 (nginx default)
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
