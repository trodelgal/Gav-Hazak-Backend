# Use the official Node.js image
FROM node:16-alpine as development

# Set working directory
WORKDIR /app

# Copy package.json and package-lock.json to install dependencies
COPY package*.json .

# Install dependencies
RUN npm install

# Copy the rest of the application code
COPY . .

RUN npm run build

FROM node:16-alpine as production

ARG NODE_ENV=production
ENV NODE_ENV=${NODE_ENV}

# Set working directory
WORKDIR /app

# Copy package.json and package-lock.json to install dependencies
COPY package*.json ./

# Install dependencies
RUN npm ci --only=production

# Copy the rest of the application code
COPY --from=development /app/dist ./dist

# Expose the port your app runs on
EXPOSE 8080

# Run the application
CMD ["node", "dist/index.js"]
