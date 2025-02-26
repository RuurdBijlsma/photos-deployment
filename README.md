# Ruurd Photos

This repository contains the deployment configuration for a self-hosted photo management system, similar to Google
Photos. It uses a Docker Compose file to orchestrate the following services:

- **Frontend** (Vue 3)
- **Backend** (Rust, built with Loco)
- **Image-Processing Service** (FastAPI)
- **Postgres** (with pgvector)
- **Nginx** (for hosting thumbnails, and reverse proxy)

The individual repositories for the frontend, backend and image-processing service are included as Git submodules.

## Prerequisites

- **Git:** To clone the repository and its submodules.
- **Docker:** Ensure Docker is installed and running.
- **Docker Compose:**

## Cloning the Repository

Clone the repository along with its submodules:

```bash
git clone --recurse-submodules https://github.com/RuurdBijlsma/photos-deployment
```

## Starting the Application

Navigate to the repository root where the docker-compose.yml file is located.

Build and start all services using Docker Compose:

```bash
docker-compose up --build
```

This command will build the necessary images (if not already built) and start the containers.

## Service Details

* **Frontend:**
    * A Vue 3 frontend.
* **Backend:**
    * The Rust/Loco backend. It connects to the image-processing service and the Postgres database.
* **Image-Processing Service:**
    * Analyzes images using machine learning methods and file metadata
    * Generates thumbnails for photos and videos.
* **Postgres:**
    * Database with support for embedding vectors through the pgvector extension.

## Configuration

Copy the `example.env` file to `.env` and configure the fields.

## Updating Submodules

If there are updates in the submodule repositories, you can pull the latest changes by running:

```bash
git submodule update --remote
```

Then commit the updated submodule pointers.

## Troubleshooting

### Containers Not Starting:

Check the container logs using docker-compose logs <service-name>.