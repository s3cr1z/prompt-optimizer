# Development Guide

## Table of Contents

- [Local Development Environment Setup](#local-development-environment-setup)
- [Docker Development and Deployment](#docker-development-and-deployment)
- [Environment Variable Configuration](#environment-variable-configuration)
- [Development Workflow](#development-workflow)
- [Project Build and Deployment](#project-build-and-deployment)
- [Troubleshooting Common Issues](#troubleshooting-common-issues)

## Local Development Environment Setup

### Basic Environment Requirements
- Node.js >= 18
- pnpm >= 8
- Git >= 2.0
- VSCode (Recommended)

### Development Environment Setup
```bash
# 1. Clone the project
git clone https://github.com/linshenkx/prompt-optimizer.git
cd prompt-optimizer

# 2. Install dependencies
pnpm install

# 3. Start development server
pnpm dev               # Main development command: build core/ui and run web app
pnpm dev:web          # Run web app only
pnpm dev:fresh        # Complete reset and restart development environment
```

## Docker Development and Deployment

### Environment Requirements
- Docker >= 20.10.0

### Docker Build and Run

#### Basic Build
```bash
# Get version number from package.json
VERSION=$(node -p "require('./package.json').version")

# Build image (using dynamic version number)
docker build -t linshen/prompt-optimizer:$VERSION .

# Add latest tag
docker tag linshen/prompt-optimizer:$VERSION linshen/prompt-optimizer:latest

# Run container
docker run -d -p 80:80 --restart unless-stopped --name prompt-optimizer -e ACCESS_PASSWORD=1234!@#$  linshen/prompt-optimizer:$VERSION


# Push
docker push linshen/prompt-optimizer:$VERSION
docker push linshen/prompt-optimizer:latest

```

Docker local build test
```shell
docker build -t linshen/prompt-optimizer:test .
docker rm -f prompt-optimizer
docker run -d -p 80:80 --restart unless-stopped --name prompt-optimizer -e VITE_GEMINI_API_KEY=111 linshen/prompt-optimizer:test

```


### Multi-stage Build Explanation

The Dockerfile uses multi-stage builds to optimize image size:

1. `base`: Basic Node.js environment, installs pnpm
2. `builder`: Build stage, installs dependencies and builds the project
3. `production`: Final image, contains only build artifacts and nginx

## Environment Variable Configuration

### Local Development Environment Variables
Create a `.env.local` file in the project root directory:

```env
# OpenAI API Configuration
VITE_OPENAI_API_KEY=your_openai_api_key

# Gemini API Configuration
VITE_GEMINI_API_KEY=your_gemini_api_key

# DeepSeek API Configuration
VITE_DEEPSEEK_API_KEY=your_deepseek_api_key

# Custom API Configuration
VITE_CUSTOM_API_KEY=your_custom_api_key
VITE_CUSTOM_API_BASE_URL=your_custom_api_base_url
VITE_CUSTOM_API_MODEL=your_custom_model_name
```

### Docker Environment Variables
Set container environment variables using the `-e` parameter:

```bash
docker run -d -p 80:80 \
  -e VITE_OPENAI_API_KEY=your_key \
  -e VITE_CUSTOM_API_BASE_URL=your_api_url \
  prompt-optimizer
```

## Development Workflow

### Code Commit Guidelines
```bash
# Commit format
<type>(<scope>): <subject>

# Example
feat(ui): Add new prompt editor component
fix(core): Fix API call timeout issue
```

### Testing Process
```bash
# Run all tests
pnpm test

# Run tests for a specific package
pnpm test:core
pnpm test:ui
pnpm test:web
```

## Project Build and Deployment

### Local Build
```bash
# Build all packages
pnpm build

# Build a specific package
pnpm build:core
pnpm build:ui
pnpm build:web
pnpm build:ext
```

### Common Docker Commands

```bash
# View container logs
docker logs -f prompt-optimizer

# Enter container
docker exec -it prompt-optimizer sh

# Container management
docker stop prompt-optimizer
docker start prompt-optimizer
docker restart prompt-optimizer

# Clean up resources
docker rm prompt-optimizer
docker rmi prompt-optimizer
```

## Troubleshooting Common Issues

### Dependency Installation Issues
```bash
# Clear dependency cache
pnpm clean

# Reinstall dependencies
pnpm install --force
```

### Development Environment Issues
```bash
# Completely reset development environment
pnpm dev:fresh

# Clear build cache
pnpm clean
rm -rf node_modules
pnpm install
```

### Build Failure Handling
1. Check if Node.js version meets requirements
2. Clear build cache: `pnpm clean`
3. Reinstall dependencies: `pnpm install`
4. View detailed build logs: `pnpm build --debug`

### Container Runtime Issues
1. Check for port conflicts: `netstat -ano | findstr :80` (Windows) or `sudo netstat -tulnp | grep :80` (Linux/macOS)
2. Check container logs: `docker logs prompt-optimizer`
3. Check container status: `docker ps -a`
