This is full source code for CareerBot version 1 as of Feb 2024. In order to run the service, you need Headai developer licence to execute API calls.

# 3AMK-AI CareerBot version 1

## Technologies

##### Frontend

React, Redux, D3js, Semantic UI

##### Backend and Database

NodeJS, ExpressJS, PostgreSQL

#### Apache, Shibboleth Service Provide (Reverse Proxy)

SAML, Apache, Docker

The application is deployed in CSC Rahti container cloud. Detail of handeling rahti container cloud is available in documentation.

## Demo

https://dev-3amk.rahtiapp.fi/

## Quick start

#### 1. Clone the Repo

```bash
$ git clone https://github.com/3amk/3amk-ai.git
```

#### 2. Install all packages for client app and server

```
cd 3amk-headai/server
$ npm install

cd 3amk-headai/app
$ npm install
```

#### 3. Add .env for both client app and server

Change to directory of server and add a file with name `.env`. Inside that file add the following:

```
EXPRESS_APP_HEADAI_TOKEN=HeadAI API token
EXPRESS_APP_LINKEDIN_ID=Linkedin oAuth client id (Auth)
EXPRESS_APP_LINKEDIN_SECRET=Linkedin oAuth sercrete (Auth)
EXPRESS_APP_LINKEDIN_REDIRECT_URI_DEV=LinkedIn redirect URL in development (http://localhost:8080/api/v1/auth/redirect/linkedin) (Auth)
EXPRESS_APP_LINKEDIN_REDIRECT_URI_PROD=LinkedIn redirect URL in production
EXPRESS_APP_GOOGLE_CLIENT_ID=Google client id for (Auth)
EXPRESS_APP_GOOGLE_CLIENT_SECRET=google oAuth client secrete (Auth)
EXPRESS_APP_GOOGLE_REDIRECT_URI_DEV=Google redirect URL in development (http://localhost:8080/api/v1/auth/redirect/google) (Auth)
EXPRESS_APP_GOOGLE_REDIRECT_URI_PROD=LinkedIn redirect URL in production
EXPRESS_APP_JWT_SECRET=JSON Web token sigining secrete (could be any sequence of characters hard to guess)
EXPRESS_APP_ENCRYPT_SECRET=random string for encrypting http payload
EXPRESS_APP_SHA_SALT=random string to encrypt user id sha

DATABASE=database name
DATABASE_USER=database user
DATABASE_PASSWORD=dabase password
DATABASE_HOST=database ip address ( for local development 127.0.0.1)
DATABASE_PORT=database port (default PostgreSQL 5432)

# for development only you can set the ip address and port to specific value, otherwise the server will run on ip 0.0.0.0 and port 8080
#LOCAL_IP=0.0.0.0
#LOCAL_PORT=8080
```

Go to the client app directory (`$3amk-headai/app`) and create `.env` file with following variables

```
REACT_APP_HEADAI_TOKEN=HeadAI API token
REACT_APP_LINKEDIN_ID=Linkedin oAuth client id (Auth)
REACT_APP_LINKEDIN_REDIRECT_URI_DEV=LinkedIn redirect URL in development (http://localhost:8080/api/v1/auth/redirect/linkedin) (Auth)
REACT_APP_LINKEDIN_REDIRECT_URI_PROD=LinkedIn redirect URL in production
REACT_APP_GOOGLE_CLIENT_ID=Google client id for (Auth)
REACT_APP_GOOGLE_REDIRECT_URI_DEV=Google redirect URL in development (http://localhost:8080/api/v1/auth/redirect/google) (Auth)
REACT_APP_GOOGLE_REDIRECT_URI_PROD=Google redirect URL in production
REACT_APP_HOTJAR_ID= Hotjar id (analytics)
REACT_APP_HOTJAR_VERSION= Hotjar version (analytics)
REACT_APP_GA_ID= Google analytics id (analytics)
INLINE_RUNTIME_CHUNK=false (to prevent embedding of script)
```

#### 4. Run the application

##### 4.1 Development mode

To run the frontend application in development mode:

Go to the app directory

```
$ cd app
```

and run the following command

```

$ npm start
```

Your react app is now running at `http://localhost:3000`

To run the backend application (server) in development mode:

Go to the server directory

```
$ cd server
```

and run the following command

```
$ npm run dev
```

the server will start at `http://localhost:8080` or at the specified `LOCAL_PORT` for development. Note that you have to update the proxy setting on `package.json` file of the React application to spcified local port.

Note: the react app will proxy all unknow requests to our server so that we can do our api request like `fetch('api/v1/users')` refer [CRA docs](https://create-react-app.dev/docs/proxying-api-requests-in-development/). This is only used on development.

##### 4.1 Production mode

To run the frontend application in production mode just build the react app by running the following command

Go to the app directory and run

```
$ npm build
```

This will produce a static file in `$3amk-headai/app/build`

To run the server application in production mode run the following command

Go to the server directory and run

```
$ npm start
```

The server will start in production mode and will serve the static build file from `$3amk-headai/app/build`

Note: The server is using ES6 modules instead CommonJS because of this Node version > 13 is expected.

#### 5. Database

The applciation uses a PostgreSQL database and the database can be run anywhere as long as it is reachable from the machine hosting our server application.

##### 5.1 local development

For connecting to the database when developing all correct database environmental variables should be provided in the `.env` file of the server application it does not matter where the database is stored as long as it is reachable. For easy of debugging and speed it is better to run the database locally when developing.

#### 5.2 Run Apache (Shibboleth SP) server

This works as a reverse proxy and is used for HAKA-login.

In folder **shibboleth-sp-docker** run:
```
$ docker-compose up
```

## 6. Project Guidelines

> refere [PROJECT GUIDELINES](./docs/PROJECT_GUIDELINES.md) document on this repo. The guidelines are subject to change according to needs of the project and opnion of developers.

## 7. Deploying / Publishing

Refere to [deployment documentation](./docs/DEPLOMENT.md) on this repo `./docs/DEPLOMENT.md`

## 8. API Reference

## 9. Tests

No tests have beeen implemented so far (both in frontend and backend)

