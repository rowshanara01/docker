# Docker Compose Cheat Sheet.

```docker
services:
  mongodb:
    image: "mongo"
    volumes:
      - ts-docker-db:/data/db
    # environment:
    #   -  MONGO_INITDB_ROOT_USERNAME=ts-docker
    #   -  MONGO_INITDB_ROOT_PASSWORD=ts-docker

    env_file:
      - ./docker-with-typescipt-backend/.env

  ts-docker-backend-container:
    build:
      context: ./docker-with-typescipt-backend
      dockerfile: Dockerfile

    ports:
      - 5000:5000

    volumes:
      - ts-docker-logs:/app/logs #named volume
      - ./docker-with-typescipt-backend:/app #bind mount
      - /app/node-modules #anonymous volume

    env_file:
      - ./docker-with-typescipt-backend/.env
    depends_on:
      - mongodb

  ts-docker-frontend-container:
    build:
      context: ./docker-with-nextjs-frontend
      dockerfile: Dockerfile

    ports:
      - 3000:3000

    volumes:
      - ./docker-with-nextjs-frontend:/app #bind mount

    env_file:
      - ./docker-with-nextjs-frontend/.env.local
    depends_on:
      - ts-docker-backend-container

volumes:
  ts-docker-db:
  ts-docker-logs:

```