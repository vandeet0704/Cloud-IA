## demo app - developing with Docker

This demo app shows a simple user profile app set up using 
- index.html with pure js and css styles
- nodejs backend with express module
- mongodb for data storage

All components are docker-based

Step 0: Get source code form the following repository:
    
    https://gitlab.com/nanuchi/developing-with-docker

![Screenshot 2024-04-23 at 1 29 07 PM](https://github.com/vandeet0704/Cloud-IA/assets/97273401/bdc2092b-d7ea-447f-8578-e6ea9a944375)

### With Docker

#### To start the application

Step 1: Create docker network

    docker network create mongo-network 

![Screenshot 2024-04-23 at 8 19 06 PM](https://github.com/vandeet0704/Cloud-IA/assets/97273401/468d1606-7b99-499a-a6f4-242ec7697584)

![Screenshot 2024-04-23 at 8 19 29 PM](https://github.com/vandeet0704/Cloud-IA/assets/97273401/1eddfbfa-fec6-46f8-82ae-306e87458558)

Step 2: start mongodb 

    docker run -d -p 27017:27017 -e MONGO_INITDB_ROOT_USERNAME=admin -e MONGO_INITDB_ROOT_PASSWORD=password --name mongodb --net mongo-network mongo   

![Screenshot 2024-04-23 at 8 38 00 PM](https://github.com/vandeet0704/Cloud-IA/assets/97273401/15ef6145-fd84-4a34-9c31-d193d7b992bc)

Step 3: start mongo-express
    
    docker run -d -p 8081:8081 -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin -e ME_CONFIG_MONGODB_ADMINPASSWORD=password --net mongo-network --name mongo-express -e ME_CONFIG_MONGODB_SERVER=mongodb mongo-express   

_NOTE: creating docker-network in optional. You can start both containers in a default network. In this case, just emit `--net` flag in `docker run` command_

![Screenshot 2024-04-23 at 8 38 47 PM](https://github.com/vandeet0704/Cloud-IA/assets/97273401/1d5df3b3-2eb3-44e6-a67a-438951106fe1)

Step 4: open mongo-express from browser

    http://localhost:8081
![Screenshot 2024-04-23 at 8 43 31 PM](https://github.com/vandeet0704/Cloud-IA/assets/97273401/2c32dfde-5425-4f6c-bf3c-9044de8358d1)

Step 5: create `user-account` _db_ and `users` _collection_ in mongo-express

![Screenshot 2024-04-23 at 8 44 37 PM](https://github.com/vandeet0704/Cloud-IA/assets/97273401/f9f79717-7959-4958-afa2-60ec46a6822f)

Step 6: Start your nodejs application locally - go to `app` directory of project 

    cd app
    npm install 
    node server.js
    
Step 7: Access you nodejs application UI from browser

    http://localhost:3000

![Screenshot 2024-04-23 at 10 35 47 PM](https://github.com/vandeet0704/Cloud-IA/assets/97273401/2406a777-ca86-43d9-8582-f4775f6e17b6)

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
