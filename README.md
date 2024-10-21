# LiLbraryManagementSystem
**library-frontend**
* this run react js application 
    - npm install 
    - npm run 
    - npm build 

all application details on `docs` folder 

__Technical stack__
* users-service: REST API
    - python
      - fast api
    - user-db:
      - postgres
* books-service: REST API
    - python
      - fast api
    - user-db:
      - postgres
* library-frontend:
    - react js

## to run the application k8s cluster 
### To run books database
    - image: postgres:15-alpine
    - environmental variables:
        -  POSTGRES_USER: user
        -  POSTGRES_PASSWORD: password
        -  POSTGRES_DB: booksdb
    - port: 5432
__To run books service__

    - image: shaikkhajaibrahim/libbookssvc:1.0
    - environmental variables:
        - DATABASE_URL: “postgresql://:@:5432/“
        - SECRET_KEY: ‘YtDEVWnL35aAIP-5yxeLjAZ49R920-mMNDfwPyWULu63HFsYzo0f-LO2InxC8eu428k’
    - port: 8000
  
__To run user database__
    - image: postgres:15-alpine
    - environmental variables:
        - POSTGRES_USER: user
        - POSTGRES_PASSWORD: password
        - POSTGRES_DB: usersdb
    - port: 5432
__To run users servics:__

    - image: shaikkhajaibrahim/libuserssvc:1.0
    - environmental variables:
        - DATABASE_URL: “postgresql://:@:5432/“
        - SECRET_KEY: ‘YtDEVWnL35aAIP-5yxeLjAZ49R920-mMNDfwPyWULu63HFsYzo0f-LO2InxC8eu428k’
    - port: 8000
  
__To run library webstore__

    - image: shaikkhajaibrahim/libwebstore:1.0
    - environmental variables
        - REACT_APP_BACKEND_API_URL: http://:8000/api/v1
        - REACT_APP_BOOKS_API_URL: http://:8000/api/v1/books
        - REACT_APP_USERS_API_URL: http://:8000/api/v1/users
    - port: 3000