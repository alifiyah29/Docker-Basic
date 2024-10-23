# Basic Node.js Docker Project

A simple Node.js application containerized with Docker. This project demonstrates how to dockerize a basic Node.js/Express application that serves "Hello World".

## Prerequisites

Before you begin, ensure you have the following installed:
- [Node.js](https://nodejs.org/) (v20 or higher)
- [Docker](https://www.docker.com/get-started)
- [Git](https://git-scm.com/) (optional)

## Project Structure

```plaintext
.
├── server.js           # Main application file
├── package.json        # Node.js dependencies and scripts
├── Dockerfile         # Docker image configuration
├── .dockerignore      # Files to exclude from Docker build
└── README.md          # This file
```

## Application Details

The application is a simple Express.js server that:
- Runs on port 8080
- Responds with "Hello World" on the root endpoint
- Listens on all network interfaces

## Getting Started

### 1. Clone the repository (or create these files in your directory)

```bash
git clone <your-repository-url>
cd <project-directory>
```

### 2. Install dependencies
```bash
npm install
```

### 3. Build the Docker image
```bash
docker build -t node_test:1.0.0 .
```

### 4. Run the container
```bash
docker run -p 3000:8080 node_test:1.0.0
```

### 5. Access the application
Open your web browser and navigate to:
```
http://localhost:3000
```

## Docker Configuration

### Dockerfile
```dockerfile
FROM node:20

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install

COPY . .

EXPOSE 8080

CMD ["node", "server.js"]
```

### .dockerignore
```plaintext
node_modules
npm-debug.log
```

## Development

To run the application locally without Docker:
```bash
node server.js
```
Then access the application at `http://localhost:8080`

## Docker Commands

Useful Docker commands for managing the application:

```bash
# List all containers (including stopped)
docker ps -a

# Stop a container
docker stop <container-id>

# Remove a container
docker rm <container-id>

# Remove an image
docker rmi node_test:1.0.0

# Build image with a different tag
docker build -t node_test:2.0.0 .

# Run container in detached mode
docker run -d -p 3000:8080 node_test:1.0.0
```

## Troubleshooting

1. **Port already in use**
   - Try a different port mapping: `docker run -p 3001:8080 node_test:1.0.0`
   - Check for running containers: `docker ps`

2. **Cannot remove image**
   - Stop and remove containers using the image first:
     ```bash
     docker stop $(docker ps -a -q)
     docker rm $(docker ps -a -q)
     ```

3. **Container exits immediately**
   - Check logs: `docker logs <container-id>`
   - Ensure server.js is properly configured

## License

ISC

## Contributing

1. Fork the repository
2. Create your feature branch
3. Commit your changes
4. Push to the branch
5. Create a new Pull Request