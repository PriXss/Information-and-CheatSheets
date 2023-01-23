
## Beispiel einer Docker-Compose File

```docker-compose
version: "3.0"
services:
  frontend:
    build:
      context: ./frontend
      dockerfile: Dockerfile.dev
    ports:
      - "3000:3000"
    container_name: mern-frontend
    # networks:
    #   - mern-stack-net
    volumes:
      - ./frontend/src:/app/src
      - ./frontend/public:/app/public
    # depends_on:
    #   - backend-one
    stdin_open: true
    tty: true
    # links:
    #   - nginx
  
  # backend-one:
  #   build:
  #     context: ./backend
  #     dockerfile: Dockerfile.dev
  #   expose:
  #     - "3001"
  #   container_name: backend-one
  #   networks:
  #     - mern-stack-net
  #   # volumes:
  #   #   - ./backend:/app
  #   # depends_on:
  #   #   - db
  #   restart: on-failure
  #   stdin_open: true
  #   tty: true
  
  backend:
    build:
      context: ./backend
      dockerfile: Dockerfile.dev
    expose:
      - "3001"
    container_name: backend
    # networks:
    #   - mern-stack-net
    volumes:
      - ./server:/app
    # depends_on:
    #   - db
    restart: on-failure
    stdin_open: true
    tty: true
    # links:
    #   - redis

#   backend-three:
#     build:
#       context: ./backend
#       dockerfile: Dockerfile.dev
#     expose:
#       - "3001"
#     container_name: backend-three
#     networks:
#       - mern-stack-net
#     volumes:
#       - ./server:/app
#     depends_on:
#       - db
#     restart: on-failure
#     stdin_open: true
#     tty: true
#     links:
#       - redis
    
#   backend-four:
#     build:
#       context: ./backend
#       dockerfile: Dockerfile.dev
#     expose:
#       - "3001"
#     container_name: backend-four
#     networks:
#       - mern-stack-net
#     volumes:
#       - ./server:/app
#     depends_on:
#       - db
#     restart: on-failure
#     stdin_open: true
#     tty: true
#     links:
#       - redis

  # db:
  #   image: mongo:latest
  #   ports:
  #     - "27017:27017"
  #   container_name: mongo-db
    # networks:
    #   - mern-stack-net
    # volumes:
    #   - mongo-data:/data/db

#   prometheus:
#     image: prom/prometheus:latest
#     container_name: prometheus
#     networks:
#       - mern-stack-net
#     ports: 
#       - "9090:9090"
#     volumes:
#       - ./prometheus:/etc/prometheus/
#       - prometheus-data:/prometheus
#     restart: always
#     command: "--config.file=/etc/prometheus/prometheus.yml"

#   nginx:
#     image: nginx:latest
#     volumes:
#       - ./nginx.conf:/etc/nginx/nginx.conf:ro
#       - ./frontend/build:/usr/share/nginx/html
#       - ./ssl:/usr/share/nginx/ssl
#     links:
#       - backend-one
#       - backend-two
#       - backend-three
#       - backend-four
#     ports:
#       - "8080:8080"
#     container_name: nginx
#     networks:
#       - mern-stack-net

#   redis:
#     image: redis:latest
#     expose:
#       - "6379"
#     container_name: redis
#     networks:
#       - mern-stack-net

# networks:
#   mern-stack-net:
#     driver: bridge

# volumes:
#   mongo-data:
#     driver: local
#   prometheus-data:
```

Hier finden wir Beispiele einer Docker-Compose File für NginX, Redis, Prometheus und Fonrt- udn Backend services.

- Volumes und persistenter Speicher sind enthalten
- Networking zwischen Containern
- MongoDB Container