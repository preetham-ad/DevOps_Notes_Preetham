# Understanding Docker Multi-Stage Builds

## Question

In Docker, the concept of which stage is considered the "final" image is tied to the process of building and tagging the image. Here’s how Docker handles this:

## How Docker Handles Multi-Stage Builds

### Dockerfile Stages

In a multi-stage Dockerfile, each `FROM` instruction starts a new stage. Docker uses the names (aliases) you provide with `AS` to refer to different stages. However, Docker doesn't explicitly mark any stage as "final" within the Dockerfile itself.

### Build Process

During the build process, Docker executes all instructions in the Dockerfile sequentially. Docker creates a series of intermediate images from each stage, but only the last stage in the Dockerfile becomes part of the final image.

### Final Image

- **Last Stage is the Final Image**: The final Docker image that gets created and tagged is derived from the last `FROM` instruction in the Dockerfile. This means that whatever is in the final stage of the Dockerfile is what ends up in the final Docker image.
- **Intermediate Stages**: Docker builds intermediate images for each stage but doesn’t keep them unless explicitly tagged. These stages are used to compile the application or prepare artifacts but aren’t part of the final image.

## Example: Multi-Stage Dockerfile

Let’s look at a multi-stage Dockerfile example:

```dockerfile
# Build Stage
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
## Step-by-Step Explanation
**Build Stage**:
Command: ```FROM node:14 AS build```
Description: Sets up the environment to build the application. It includes all build tools and dependencies.
Intermediate Image: This stage produces an intermediate image named build (by the alias AS build), which contains the application code and built artifacts.

## Runtime Stage:
Command: ```FROM node:14-slim```
Description: This is a new stage that starts from a smaller, slimmer base image. It copies the build artifacts from the build stage.
Final Image: This is the stage from which the final Docker image is created. The COPY --from=build instructions pull in only the necessary files from the build stage.

# How Docker Determines the Final Image:
**Execution Order**: Docker processes the stages in order. The last FROM statement (FROM node:14-slim) defines the base for the final image.
**Tagging**: When you run docker build -t myapp:multi ., Docker builds the image based on the instructions from the final stage (node:14-slim). The result is tagged as myapp:multi.
**Intermediate Stages**: The intermediate stages (like the build stage) are used during the build process but are not part of the final image unless specifically tagged.

# How to Check the Final Image
**List Docker Images:**

```bash
Copy code
docker images
```
This command lists all images. You’ll see your final image (myapp:multi) with its size and other details.

**Inspect the Final Image:**

```bash
Copy code
docker history myapp:multi
```
This command shows the history of layers in the image, which helps you understand what’s included in the final image.

**Run the Image:**

```bash
Copy code
docker run -d -p 3000:3000 myapp:multi
```
Running the final image shows the container with only the necessary runtime components.
