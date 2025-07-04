FROM node:18-alpine

WORKDIR /app

# Copy only package.json first
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the code
COPY . .

# Run the gateway
CMD ["node", "index.js"]
