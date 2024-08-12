# Understanding Docker Multi-Stage Builds

## Key Concepts

### Dockerfile Structure
- **Regular Dockerfile**: Contains all commands for building and running the application in a single image.
- **Multi-Stage Dockerfile**: Separates the build and runtime stages into distinct stages.

### Image Layers
- Docker images are built in layers. Each `RUN`, `COPY`, or `ADD` instruction creates a new layer in the image.

## Breakdown of How Multi-Stage Builds Work

### Regular Dockerfile

**Dockerfile:**

```dockerfile
# Regular Dockerfile
FROM node:14

WORKDIR /app

COPY package.json package-lock.json ./
RUN npm install

COPY . .
RUN npm run build

CMD ["node", "dist/server.js"]
```
## What Happens:

- **Base Image**: node:14 is used as the base image. This image includes Node.js and npm.
- **Dependencies**: npm install adds all dependencies, including build tools.
- **Code and Build**: Copies the source code and builds it. The build tools and intermediate files are still part of the image.
- **Final Image**: Includes Node.js, all dependencies, the source code, build tools, and the built application. This results in a larger image (e.g., 1 GB).

## Issues:
The final image contains everything needed for both building and running the application, including:
Build tools (npm, Node.js)
Source code
Built application

## Multi-Stage Dockerfile
```# Build Stage
FROM node:14 AS build

WORKDIR /app

COPY package.json package-lock.json ./
RUN npm install

COPY . .
RUN npm run build

# Runtime Stage
FROM node:14-slim

WORKDIR /app

COPY --from=build /app/dist /app/dist
COPY --from=build /app/package.json /app/package-lock.json /app/

RUN npm install --production

CMD ["node", "dist/server.js"]
```

## What Happens:

**Build Stage**:
- Uses node:14 image to compile the application.
- Installs all build tools and dependencies.
- Copies the source code and builds the application.
- This stage is not included in the final image; it's just used to prepare the build artifacts.

**Runtime Stage**:
- Uses node:14-slim, a smaller base image without build tools.
- Copies only the necessary artifacts from the build stage:
- Built application (/app/dist)
- Production dependencies
- Installs only production dependencies (no development dependencies or build tools).

**Why the Image is Reduced**:
- Lighter Base Image: The runtime stage uses a slimmer base image (node:14-slim) that doesn’t include build tools or unnecessary components.
- Selective Copy: Only the essential files (compiled code and runtime dependencies) are copied from the build stage.
- No Build Tools: The final image doesn’t include any build tools or intermediate files, just the runtime environment and the application.

## Example Comparison:
- **Regular Dockerfile**: The final image might be around 1 GB due to the inclusion of all build tools, source code, and the built application.
- **Multi-Stage Dockerfile**: The final image might be reduced to around 200 MB because it only contains the built application and production dependencies, with a much smaller base image.
