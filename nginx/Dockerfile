# Stage 1: Build the frontend
FROM node:23 AS builder

WORKDIR /app

# Copy package.json and package-lock.json to leverage Docker caching
COPY photos-frontend/package.json photos-frontend/package-lock.json ./

RUN npm install --frozen-lockfile

# Copy the rest of the frontend code and build
COPY photos-frontend ./

RUN chmod -R a+x node_modules
RUN npm run build

# Stage 2: Serve with Nginx
FROM nginx:latest

WORKDIR /usr/share/nginx/html

# Copy the built frontend from the previous stage
COPY --from=builder /app/dist /usr/share/nginx/html

# Remove default Nginx config and replace it with a custom one
RUN rm /etc/nginx/conf.d/default.conf
COPY api.conf /etc/nginx/conf.d/default.conf

# Expose the default HTTP port
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
