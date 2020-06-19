# Multiple Server On One VPS With Docker and Nginx
==================================================

### `docker network create nginx-proxy`

### `docker-compose up -d`

### Create server with enviroment variable: VIRTUAL_HOST, VIRTUAL_PORT, LETSENCRYPT_HOST, LETSENCRYPT_HOST

### Example:
```
    version: "3"

    services:
      examle_container:
        build:
          context: .
          dockerfile: Dockerfile
        container_name: examle_container
        restart: unless-stopped
        environment:
          VIRTUAL_HOST: abc.website.com
          VIRTUAL_PORT: 4567
          LETSENCRYPT_HOST: abc.website.com
          LETSENCRYPT_HOST: abcowner@email.com

        ports:
          - 4567:4567
        volumes:
          - .:/app
          - /app/node_modules
          - ./build:/app/build
          - ./public:/app/public
        expose:
          - 4567
        command: npm run start

    volumes:
      node_modules:

    networks:
      default:
        external:
          name: nginx-proxy
```
