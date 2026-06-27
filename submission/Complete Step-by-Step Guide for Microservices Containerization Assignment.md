Complete Step-by-Step Guide for Microservices Containerization Assignment

Prerequisites Software Versions:
Docker: Version 29.5.3
Node.js: Version v24.18.0
npm: Version 11.16.0
Git: Version 2.53.0.windows.2

Step 1: Fork and Clone the Repository
Action:
git clone https://github.com/rahatpal/Rahat-s-Microservices-Task.git
cd "Rahat-s-Microservices-Task"
Expected Result:
You'll have a local copy of the repository with three microservice folders.

Step 2: Analyze Service Structure
Action:
Examine each service directory structure:

ls -Path .\user-service\
ls -Path .\product-service\  
ls -Path .\gateway-service\
ls -Path .\order-service\
Expected Result:
You'll see package.json, app.js or app.js files and other source code in each directory.

Step 3: Create Dockerfiles for Each Service
For User Service (user-service/Dockerfile):
FROM node:16-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 3000

CMD ["node", "app.js"]

For Product Service (product-service/Dockerfile):
FROM node:16-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 3001

CMD ["node", "app.js"]

For Gateway Service (gateway-service/Dockerfile):
FROM node:16-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 3003

CMD ["node", "app.js"]

For Order Service (order-service/Dockerfile):
FROM node:16-alpine

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 3002

CMD ["node", "app.js"]






Step 4: Create docker-compose.yml
Action:
Create docker-compose.yml in the root directory:

services:
  user-service:
    build: ./user-service
    ports:
      - "3000:3000"
    networks:
      - microservice-network
    restart: unless-stopped

  product-service:
    build: ./product-service
    ports:
      - "3001:3001"
    networks:
      - microservice-network
    restart: unless-stopped

  order-service:
    build: ./order-service
    ports:
      - "3002:3002"
    networks:
      - microservice-network
    restart: unless-stopped

  gateway-service:
    build: ./gateway-service
    ports:
      - "3003:3003"
    networks:
      - microservice-network
    depends_on:
      - user-service
      - product-service
      - order-service
    restart: unless-stopped

networks:
  microservice-network:
    driver: bridge

Step 5: Create Submission Directory Structure
Action:
mkdir "submission"
mkdir "submission\user-service"
mkdir "submission\product-service" 
mkdir "submission\order-service"
mkdir "submission\gateway-service"

Step 6: Copy Files to Submission Directory
Action:
# Copy Dockerfiles
Copy-Item -Path ".\user-service\Dockerfile" -Destination ".\submission\user-service\"
Copy-Item -Path ".\product-service\Dockerfile" -Destination ".\submission\product-service\"
Copy-Item -Path ".\order-service\Dockerfile" -Destination ".\submission\order-service\"
Copy-Item -Path ".\gateway-service\Dockerfile" -Destination ".\submission\gateway-service\"

# Copy docker-compose.yml
Copy-Item -Path ".\docker-compose.yml" -Destination ".\submission\"

Step 7: Verify Directory Structure
Action:
ls -Path .\submission\
ls -Path .\submission\user-service\
ls -Path .\submission\product-service\
ls -Path .\submission\order-service\
ls -Path .\submission\gateway-service\
Expected Result:
submission/
├── user-service/
│   └── Dockerfile
├── product-service/  
│   └── Dockerfile
├── order-service/
│   └── Dockerfile
├── gateway-service/
│   └── Dockerfile
└── docker-compose.yml





Step 8: Build and Run Services
Action:
# Navigate to submission directory
cd .\submission\

# Build and start all services
docker-compose up –build







Step 9: Test the Services
Action:
Open a new PowerShell window and test each service:
# Test user service
curl http://localhost:3000/users

# Test product service  
curl http://localhost:3001/products

# Test order service
curl http://localhost:3002/orders

# Test gateway service
curl http://localhost:3003/health


Step 10: Stop Services
Action:
In the original PowerShell window where docker-compose is running, press Ctrl+C to stop the services.

Step 11: Verify Container Status
Action:
# Check running containers
docker ps

# Check all containers (including stopped)
docker ps -a

Step 13: Final Verification
Action:
Verify everything is working properly:

# Check Docker version
docker --version

Troubleshooting Tips
If Docker commands fail:
Ensure Docker Desktop is running
Restart PowerShell/Command Prompt
Run as Administrator if needed
If ports are in use:
# Change port mappings in docker-compose.yaml
# Example: 3004:3000 instead of 3000:3000
If services don't start:
# Check logs for errors
docker-compose logs

# Rebuild services
docker-compose build --no-cache
docker-compose up
This complete guide now includes the missing order service and provides a comprehensive workflow for your microservices containerization assignment, using your exact software versions!