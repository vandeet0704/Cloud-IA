## demo app - developing with Docker

This demo app shows a simple user profile app set up using 
- index.html with pure js and css styles
- nodejs backend with express module
- mongodb for data storage

All components are docker-based

Step 0: Get source code form the following repository:
    
    https://gitlab.com/nanuchi/developing-with-docker
![git-clone](https://github.com/vandeet0704/Cloud-IA/blob/main/app/images/Screenshot%202024-04-23%20at%201.29.07%20PM.png)

### With Docker

#### To start the application

Step 1: Create docker network

    docker network create mongo-network 

![create-network](https://github.com/vandeet0704/Cloud-IA/blob/main/app/images/Screenshot%202024-04-23%20at%208.19.06%20PM.png)

![list_networks](https://github.com/vandeet0704/Cloud-IA/blob/main/app/images/Screenshot%202024-04-23%20at%208.19.29%20PM.png)

Step 2: start mongodb 

    docker run -d -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password --name mongodb --net mongo-network mongo   

![mongo-image](https://github.com/vandeet0704/Cloud-IA/blob/main/app/images/Screenshot%202024-04-23%20at%208.38.00%20PM.png)

Step 3: start mongo-express
    
    docker run -d -p 8081:8081 -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin -e ME_CONFIG_MONGODB_ADMINPASSWORD=password --net mongo-network --name mongo-express -e ME_CONFIG_MONGODB_SERVER=mongodb mongo-express   

_NOTE: creating docker-network in optional. You can start both containers in a default network. In this case, just emit `--net` flag in `docker run` command_

![express-image](https://github.com/vandeet0704/Cloud-IA/blob/main/app/images/Screenshot%202024-04-23%20at%208.38.47%20PM.png)

Step 4: open mongo-express from browser

    http://localhost:8081
![login](https://github.com/vandeet0704/Cloud-IA/blob/main/app/images/Screenshot%202024-04-23%20at%208.43.31%20PM.png)

Step 5: create `user-account` _db_ and `users` _collection_ in mongo-express

![create-db](https://github.com/vandeet0704/Cloud-IA/blob/main/app/images/Screenshot%202024-04-23%20at%208.44.37%20PM.png)

Step 6: Start your nodejs application locally - go to `app` directory of project 

    cd app
    npm install 
    node server.js
    
Step 7: Access you nodejs application UI from browser

    http://localhost:3000

![app](https://github.com/vandeet0704/Cloud-IA/blob/main/app/images/Screenshot%202024-04-23%20at%2010.35.47%20PM.png)

### With Docker Compose

#### To start the application

Step 1: start mongodb and mongo-express

    docker-compose -f docker-compose.yaml up
    
_You can access the mongo-express under localhost:8080 from your browser_
    
Step 2: in mongo-express UI - create a new database "my-db"

Step 3: in mongo-express UI - create a new collection "users" in the database "my-db"       
    
Step 4: start node server 

    cd app
    npm install
    node server.js
    
Step 5: access the nodejs application from browser 

    http://localhost:3000

#### To build a docker image from the application

    docker build -t my-app:1.0 .       


The dot "." at the end of the command denotes location of the Dockerfile.
# Initial commit
