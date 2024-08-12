# Understanding Docker Builds and Multi-Stage Builds

## What is a Docker Container?

A Docker container is like a self-contained box that includes everything needed to run an application:
- **Code**: The application code.
- **Dependencies**: Libraries and other requirements.
- **Runtime**: The environment needed to run the application.
- **System Libraries**: Operating system components.

The goal of Docker is to ensure the application runs the same way on any machine, removing the "it works on my machine" problem.

## Build vs. Runtime

- **Build**:
  - **What it is**: The process of preparing your application. This includes compiling code, installing libraries, and setting up configurations.
  - **Analogy**: Think of it like cooking a meal. You need all the ingredients and tools to prepare the dish.

- **Runtime**:
  - **What it is**: The phase when you actually run the application. At this stage, you only need the finished product, not the tools or ingredients used to make it.
  - **Analogy**: Serving the cooked meal. You just need the meal itself, not the recipe or cooking tools.

## Why Use Docker for Both Build and Run?

- **Consistency**: Docker ensures that the environment used for building and running your application is consistent. This helps your application work the same way everywhere.

- **Build Dockerfile**: Used to create the application package. It includes tools and dependencies required for building the application.

- **Runtime Dockerfile**: Used to run the application. It should be minimal, containing only what’s needed to execute the application.

## Single-Stage Docker Build

In a single-stage Docker build, everything is included in one image:

```dockerfile
# Single-Stage Dockerfile
FROM node:14

WORKDIR /app
COPY package.json package-lock.json ./
RUN npm install
COPY . .
RUN npm run build

CMD ["node", "dist/server.js"]
```
## Problems with Single-Stage Build:

- Image Size: Includes build tools and dependencies not needed at runtime.
- Security: Extra tools can be potential security risks.
- Performance: Larger images can be slower to deploy and transfer.

## Multi-Stage Docker Build
A multi-stage Docker build allows you to use multiple FROM statements in a single Dockerfile. Each FROM statement begins a new stage in the build process. This approach enables you to create different stages for building and running your application, which can help in reducing the final image size and improving security.

The term "multi-stage Docker build" refers to a Dockerfile technique where multiple stages are used to build an application, but only the final stage contains the minimal runtime environment needed to run the application.

# FROM statements in MSDB 
If you are using multi-stage builds, each FROM statement denotes the beginning of a new stage. You can copy artifacts from one stage to another, allowing you to use a lightweight image for the final stage and a more feature-rich image for the build stage.

```
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

## Benefits of Multi-Stage Builds:

**Reduce Image Size**:
- Build Stage: Includes tools needed to build the application.
- Runtime Stage: Only includes the final application and runtime dependencies. This results in a smaller, leaner image.

**Improve Security**:
The final image does not include build tools or unnecessary files, reducing potential security risks.

**Simplify Image Management**:
The final image is cleaner and easier to manage because it only contains what's necessary to run the application.
## Summary
**Docker Container**: Ensures consistency across different environments by bundling everything needed to run an application.

**Build Stage**: Prepares the application (like cooking the ingredients).

**Runtime Stage**: Runs the application (like serving the meal).

**Multi-Stage Build**: Uses separate stages to build and run the application, resulting in smaller, more secure, and efficient images.
