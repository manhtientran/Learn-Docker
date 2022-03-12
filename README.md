# Learn developing application with Docker

This application contains:

- index.html with pure js and css
- node.js with express framework
- database: MongoDB

All components are docker-based

## With Docker

Step 1: Create docker network

    docker network create mongo-network

Step 2: Start MongoDB

    docker run -d \
    -p 27017:27017 \
    -e MONGO_INITDB_ROOT_USERNAME=admin \
    -e MONGO_INITDB_ROOT_PASSWORD=password \
    --name mongodb \
    --net mongo-network \
    mongo

Step 3: Start Mongo-Express

    docker run -d \
    -p 8081:8081 \
    -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
    -e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
    --net mongo-network \
    --name mongo-express \
    -e ME_CONFIG_MONGODB_SERVER=mongodb \
    mongo-express

\_NOTE: creating docker network is optional. You can start
both containers in a default network. In this case, just omit
`--net` flag in `docker run` command

Step 4: Open mongo-express from browser

    http://localhost:8081

Step 5: Create `user-account` _db_ and `user` _collection_
in mongo-express

Step 6: Start your Node.js application locally - go to `app`
directory of project

    npm install
    node server.js

Step 7: Access your Node.js application from your browser

    http://localhost:3000

## With Docker Compose

Step 1: Start MongoDB and Mongo-Express

    docker-compose -f docker-compose.yaml up

_You can access the Mongo-Express from localhost:8080 in your browser_

Step 2: In Mongo-Express UI - create a new database "my-db"

Step 3: In Mongo-Express UI - create a new collection "users"
in the database "my-db"

Step 4: Start Node server

    npm install
    node server.js

Step 5: Access the Node.js application from browser

    http:localhost:3000

## To build a Docker Image from the application

    docker build -t my-app:1.0 .

The dot "." at the end of the command denotes location of
the Docker file
