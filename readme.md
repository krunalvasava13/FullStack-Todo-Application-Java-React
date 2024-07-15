# Full Stack Application with Spring Boot and React js


<img src="react_00_architecture.png" width="300">

# <a href="http://todo-fullstack-krunal.s3-website.ap-south-1.amazonaws.com/" style="display: inline-block; padding: 10px 20px; font-size: 18px; color: white; background-color: #4CAF50; text-align: center; text-decoration: none; border-radius: 5px;">Live Demo</a>


## Running the Application

- REST API - Import into Eclipse as Maven Project. Run `com.krunal139.rest.webservices.restfulwebservices.RestfulWebServicesApplication` as a Java Application. Check Authentication and REST API Sections for executing REST APIs.
- React Application - Import `frontend/todo-app` into Visual Studio Code. Run `npm install` followed by `npm start`
- http://localhost:3000/ with credentials in28minutes/dummy



## Deploying Front End to AWS

### Change /04-frontend/todo-app/src/components/todo/api/ApiClient.js

```
export const apiClient = axios.create(
    {
        baseURL: 'http://localhost:5000' //#CHANGE
    }
);

/* For Best Practices https://facebook.github.io/create-react-app/docs/adding-custom-environment-variables*/

```

### Create Production Build

`npm run build`


### S3 Access for Static Content

```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AddPerm",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::YOUR-BUCKET-NAME/*"
        }
    ]
}
```

## Authentication

All REST API are protected by JWT Authentication with Spring Security. 

POST to http://localhost:5000/authenticate

```
{
  "username":"user",
  "password":"pwd1"
}
```

Response
```
{
"token": "eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJpbjI4bWludXRlcyIsImV4cCI6MTU2MjIzNDM1OSwiaWF0IjoxNTYxNjI5NTU5fQ.yvkFtYAp8yGClDo7D5wtXyPSnUPtxu8A7A9YCl9FJdjR0di_yAaPcSTR6liN5bIu1SnOJuSZp94pYSYzU_BNEw" //use your token
}
```

Use the token in the headers for all subsequent requests.

`Authorization` : `Bearer ${token}`

Example 

`Authorization` : `Bearer eyJhbGciOiJIUzUxMiJ9.eyJzdWIiOiJpbjI4bWludXRlcyIsImV4cCI6MTU2MjIzNDM1OSwiaWF0IjoxNTYxNjI5NTU5fQ.yvkFtYAp8yGClDo7D5wtXyPSnUPtxu8A7A9YCl9FJdjR0di_yAaPcSTR6liN5bIu1SnOJuSZp94pYSYzU_BNEw`



## Hello World URLS

- http://localhost:5000/hello-world

```txt
Hello World
```

- http://localhost:5000/hello-world-bean

```json
{"message":"Hello World - Changed"}
```

- http://localhost:5000/hello-world/path-variable/krunal

```json
{"message":"Hello World, krunal"}
```

## TODO Resource Details

- GET - http://localhost:5000/users/user/todos

```
[
  {
    "id": 10001,
    "username": "user",
    "description": "Learn JPA",
    "targetDate": "2019-06-27T06:30:30.696+0000",
    "done": false
  },
  {
    "id": 10002,
    "username": "user",
    "description": "Learn Data JPA",
    "targetDate": "2019-06-27T06:30:30.700+0000",
    "done": false
  },
  {
    "id": 10003,
    "username": "user",
    "description": "Learn Microservices",
    "targetDate": "2019-06-27T06:30:30.701+0000",
    "done": false
  }
]
```

#### Retrieve a specific todo

- GET - http://localhost:5000/users/user/todos/10001

```
{
  "id": 10001,
  "username": "user",
  "description": "Learn JPA",
  "targetDate": "2019-06-27T06:30:30.696+0000",
  "done": false
}
```

#### Creating a new todo

- POST to http://localhost:5000/users/user/todos with BODY of Request given below

```
{
  "username": "user",
  "description": "Learn to Drive a Car",
  "targetDate": "2030-11-09T10:49:23.566+0000",
  "done": false
}
```

#### Updating a new todo

- http://localhost:5000/users/user/todos/10001 with BODY of Request given below

```
{
  "id": 10001,
  "username": "user",
  "description": "Learn to Drive a Car",
  "targetDate": "2045-11-09T10:49:23.566+0000",
  "done": false
}
```

#### Delete todo

- DELETE to http://localhost:5000/users/user/todos/10001


## H2 Console

- http://localhost:5000/h2-console
- Use `jdbc:h2:mem:testdb` as JDBC URL 

