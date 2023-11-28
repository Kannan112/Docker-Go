# Dockerfile for Docker Swarm setup

### README.md (Begin) ###
RUN /bin/bash -c 'cat <<EOF >README.md

# 🐳 Docker Swarm Setup

Welcome to this repository designed to help you set up a Docker Swarm environment!

## Prerequisites

- Docker installed on your machine

## 🚀 Instructions

### Build Docker image

1. **Clone this repository:**
   \`\`\`bash
   git clone https://github.com/your-username/your-repo.git
   cd your-repo
   \`\`\`

2. **Build the Docker image:**
   \`\`\`bash
   docker build -t swarm-setup .
   \`\`\`

### Create Docker Swarm

3. **Run the Docker container to create a Docker Swarm:**
   \`\`\`bash
   docker run -d --privileged --name swarm-container swarm-setup
   \`\`\`

4. **Verify that the Docker Swarm is running:**
   \`\`\`bash
   docker -H tcp://0.0.0.0:2375 info
   \`\`\`

### Access Docker Swarm

To interact with the Docker Swarm, use the following command:
\`\`\`bash
docker -H tcp://0.0.0.0:2375 <command>
\`\`\`

Replace \`<command>\` with any Docker command you want to execute on the Swarm.

### Stop Docker Swarm

To stop the Docker Swarm container, use:
\`\`\`bash
docker stop swarm-container
\`\`\`

## ℹ️ Important Notes

- Ensure that port 2375 is accessible and properly secured if exposed to the internet.
- This setup is for educational purposes and should be used responsibly.

EOF'
### README.md (End) ###

# Use an official Docker image as the base
FROM docker:latest

# Install Docker Swarm
RUN docker run --privileged --rm docker/binfmt:a7996909642ee92942dcd6cff44b9b95f08dad64

# Set up environment variables for Swarm initialization
ENV DOCKER_HOST=tcp://0.0.0.0:2375

# Set up Docker Swarm
RUN docker swarm init --advertise-addr=eth0

# Expose the required ports
EXPOSE 2375

# Command to start Docker Swarm
CMD ["dockerd"]
