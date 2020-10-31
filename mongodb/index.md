# Mongo DB

### Sign in mongo db cli
```sh
$ mongo -u admin -p password
```

### Create a new user
```js
use myDatabase
db.createUser(
{
    user: "myUser",
    pwd: "myPassword",
    roles: [
      { role: "readWrite", db: "myDatabase" }
    ]
})
```

### Run mongodb and mongo-express with docker-compose
```yaml
# Sources:
# https://zgadzaj.com/development/docker/docker-compose/containers/mongo-express

version: '3.5'

services:
  mongodb:
    image: mongo:latest
    container_name: mongodb
    command: --auth
    restart: always
    ports:
      - 27017:27017
    volumes:
      - ./data:/data/db
#      - ./mongo-entrypoint.sh:/docker-entrypoint.sh
    environment:
      MONGO_INITDB_ROOT_USERNAME: root
      MONGO_INITDB_ROOT_PASSWORD: example

  mongo-express:
    image: mongo-express:latest
    container_name: mongo-express
    ports:
      - 8081:8081
#        volumes:
#            - ./mongo-express-entrypoint.sh:/docker-entrypoint.sh
    environment:
      ME_CONFIG_MONGODB_SERVER: mongodb
      ME_CONFIG_MONGODB_ADMINUSERNAME: root
      ME_CONFIG_MONGODB_ADMINPASSWORD: example
#      ME_CONFIG_BASICAUTH_USERNAME: ${ME_CONFIG_BASICAUTH_USERNAME}
#      ME_CONFIG_BASICAUTH_PASSWORD: ${ME_CONFIG_BASICAUTH_PASSWORD}
    depends_on:
      - mongodb
```