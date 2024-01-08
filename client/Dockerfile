# Stage 1: Build client
FROM node:14 as client-builder

WORKDIR /app/client
COPY package*.json ./

RUN npm install
COPY . .

RUN npm run build

# Stage 2: Final image
FROM node:14-alpine

WORKDIR /app

# Create a directory for the client build
RUN mkdir -p /app/client/build

# Copy only necessary files from client build
COPY --from=client-builder /app/client/build /app/client/build

# Expose the port your client app runs on
EXPOSE 3000

# Start the client application
CMD ["npx", "serve", "/app/client/build"]
