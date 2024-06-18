# How to Use Swagger with Docker


# How to Use Swagger with Docker

## Prerequisites

To follow this guide, you need:
- Docker installed on your machine.
- Docker Compose installed on your machine.

## Docker Compose File

This is an example of a Docker Compose file for Swagger Editor, Swagger UI, and Swagger Codegen. Copy this file and save it as `docker-compose.yml`:

```yaml
services:
  swagger-editor:
    image: swaggerapi/swagger-editor
    ports:
      - "8080:8080"
    environment:
      SWAGGER_FILE: /data/swagger.yml
    volumes:
      - ./data:/data

  swagger-ui:
    image: swaggerapi/swagger-ui
    ports:
      - "8081:8080"
    environment:
      SWAGGER_JSON: /data/swagger.yml
    volumes:
      - ./data:/data

  swagger-codegen:
    image: openapitools/openapi-generator-cli
    user: "1000:1000"
    volumes:
      - ./data:/data
    command: ["help"]
```

## Start / Stop container using docker compose command

1. Open a terminal and navigate to the directory where you saved the `docker-compose.yml` file.
1. Run the following command to start the services:

    ```sh
    docker-compose up -d
    docker-compose down
    ```

## Access Swagger Editor and Swagger UI
1. Open your web browser:
    - Swagger Editor: `http://localhost:8080`
    - Swagger UI: `http://localhost:8081`

Now you can edit your API definition in Swagger Editor and view it in Swagger UI.

## Generate Code with Swagger Codegen

To generate code for client, server, or documentation, follow these steps:

1. Ensure your `docker-compose.yml` file includes the `swagger-codegen` service as shown above.
2. Open a terminal and run the following command to generate code:

    ```sh
    docker compose run swagger-codegen generate --api-package 3.0.0 -i /data/swagger.yml --generator-name html2 -o /data/output
    ```

    Replace `language`, `file name` with the right `value`.

3. The generated code will be saved in the folder `./data/output`.

## Conclusion

Using Docker and Docker Compose, you can easily set up Swagger Editor, Swagger UI, and Swagger Codegen. This allows you to edit, view, and generate code from your API definitions quickly and efficiently.
