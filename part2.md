# Part 2

## 1

```yaml
version: "3.9"
services:
  simpleweb:
    image: devopsdockeruh/simple-web-service
    volumes:
      - ./text.log:/usr/src/app/text.log
```

## 2

```yaml
version: "3.9"
services:
  simpleweb:
    image: devopsdockeruh/simple-web-service
    command: server
    ports:
      - 8080:8080
```

## 3

```yaml
version: "3.9"
services:
  example-frontend:
    build:
      context: ./example-frontend
      dockerfile: Dockerfile
    ports:
      - 4000:5000
  example-backend:
    build:
      context: ./example-backend
      dockerfile: Dockerfile
    ports:
      - 8080:8080
```

## 4

```yaml
version: "3.9"
services:
  example-frontend:
    build:
      context: ./example-frontend
      dockerfile: Dockerfile
    ports:
      - 4000:5000

  example-backend:
    build:
      context: ./example-backend
      dockerfile: Dockerfile
    ports:
      - 8080:8080
    environment:
      - REDIS_HOST=redis

  redis:
    image: "redis:alpine"
    command: redis-server
    ports:
      - "6379:6379"
```

## 5

```
docker-compose up --scale compute=20
```

## 6

```yaml
version: "3.9"
services:
  example-frontend:
    build:
      context: ./example-frontend
      dockerfile: Dockerfile
    ports:
      - 4000:5000

  example-backend:
    build:
      context: ./example-backend
      dockerfile: Dockerfile
    ports:
      - 8080:8080
    environment:
      - REDIS_HOST=redis
      - POSTGRES_HOST=db
      - POSTGRES_PASSWORD=dockermoocpassword

  redis:
    image: "redis:alpine"
    command: redis-server
    ports:
      - "6379:6379"

  db:
    image: postgres
    restart: always
    environment:
      POSTGRES_PASSWORD: dockermoocpassword
```

## 7

```yaml
version: "3.9"
services:
  training:
    build:
      context: ./ml-kurkkumopo-training
      dockerfile: Dockerfile
    volumes:
      - imgs:/src/imgs
      - model:/src/model

  frontend:
    build:
      context: ./ml-kurkkumopo-frontend
      dockerfile: Dockerfile
    ports:
      - 3000:3000

  backend:
    build:
      context: ./ml-kurkkumopo-backend
      dockerfile: Dockerfile
    volumes:
      - model:/src/model:ro
    ports:
      - 5000:5000
volumes:
  imgs: null
  model: null
```

## 8

```yaml
version: "3.9"
services:
  example-frontend:
    build:
      context: ./example-frontend
      dockerfile: Dockerfile
    ports:
      - 4000:5000

  example-backend:
    build:
      context: ./example-backend
      dockerfile: Dockerfile
    ports:
      - 8080:8080
    environment:
      - REQUEST_ORIGIN=http://localhost
      - REDIS_HOST=redis
      - POSTGRES_HOST=db
      - POSTGRES_PASSWORD=dockermoocpassword

  redis:
    image: "redis:alpine"
    command: redis-server
    ports:
      - "6379:6379"

  db:
    image: postgres
    restart: always
    environment:
      POSTGRES_PASSWORD: dockermoocpassword

  web:
    image: nginx
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf:ro
    ports:
      - 80:80
```

## 9

```yaml
version: "3.9"
services:
  example-frontend:
    build:
      context: ./example-frontend
      dockerfile: Dockerfile
    ports:
      - 4000:5000

  example-backend:
    build:
      context: ./example-backend
      dockerfile: Dockerfile
    ports:
      - 8080:8080
    environment:
      - REQUEST_ORIGIN=http://localhost
      - REDIS_HOST=redis
      - POSTGRES_HOST=db
      - POSTGRES_PASSWORD=dockermoocpassword

  redis:
    image: "redis:alpine"
    command: redis-server
    ports:
      - "6379:6379"

  db:
    image: postgres
    restart: unless-stopped
    environment:
      POSTGRES_PASSWORD: dockermoocpassword
    volumes:
      - ./db_data:/var/lib/postgresql/data

  web:
    image: nginx
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf:ro
    ports:
      - 80:80
```

## 10

I made sure everything kept working while making the changes earlier, so no additional changes needed here.

`REQUEST_ORIGIN=http://localhost` for the backend was one of the important bits.

## 11

Plenty of experience in configuring containerized services at work, however, those files aren't public.

For the sake of this exercise, I added a primitive docker-compose file to <https://github.com/Walther/hello-dockermooc> toy repo.
