# Dockerized Node Js Apps

<a name="top"></a>
Topics: 

1. [Dockerized Vue Js](#vuejs_app)







[Go To Top](#top)
<a name="vuejs_app"></a>
## 1.

#### Vuejs App 

Dockerfile: 

      FROM node:lts-alpine

      # install simple http server for serving static content
      
            RUN npm install -g http-server

      # make the 'app' folder the current working directory
      
            WORKDIR /app

      # copy both 'package.json' and 'package-lock.json' (if available)
      
            COPY package*.json ./

      # install project dependencies
      
            RUN npm install

      # copy project files and folders to the current working directory (i.e. 'app' folder)
      
            COPY . .

      # build app for production with minification
      
            RUN npm run build

      EXPOSE 8080
      
            CMD [ "http-server", "dist" ]


      docker build -t vuejs-cookbook/dockerize-vuejs-app .


      docker run -it -p 8080:8080 --rm --name dockerize-vuejs-app-1 vuejs-cookbook/dockerize-vuejs-app

      We should be able to access our Vue.js app on localhost:8080.


      Let’s refactor our Dockerfile to use NGINX:


###### build stage

      FROM node:lts-alpine as build-stage
      WORKDIR /app
      COPY package*.json ./
      RUN npm install
      COPY . .
      RUN npm run build

###### production stage

      FROM nginx:stable-alpine as production-stage
      COPY --from=build-stage /app/dist /usr/share/nginx/html
      EXPOSE 80
      CMD ["nginx", "-g", "daemon off;"]


            docker build -t vuejs-cookbook/dockerize-vuejs-app .
            docker run -it -p 8080:80 --rm --name dockerize-vuejs-app-1 vuejs-cookbook/dockerize-vuejs-app


    Microservices
    DevOps
    Continuous Delivery


===> End Vuejs App <======

----------------------------------------------------------

[Go To Top](#top)
## 2.

#### React App 


      // .dockerignore
      
            node_modules
            build


// Dockerfile

#### ==== CONFIGURE =====

###### Use a Node 16 base image

      FROM node:16-alpine 
      
###### Set the working directory to /app inside the container

      WORKDIR /app
      
###### Copy app files

      COPY . .
      
###### ==== BUILD =====

###### Install dependencies (npm ci makes sure the exact versions in the lockfile gets installed)

      RUN npm ci 
      
###### Build the app

      RUN npm run build
      
###### ==== RUN =======

###### Set the env to "production"

      ENV NODE_ENV production
      
###### Expose the port on which the app will be running (3000 is the default that `serve` uses)

      EXPOSE 3000

###### Start the app

      CMD [ "npx", "serve", "build" ]



###### Build the Docker image for the current folder 
###### and tag it with `dockerized-react`

      docker build . -t dockerized-react

###### Check the image was created

      docker images | grep dockerized-react

###### Run the image in detached mode 
###### and map port 3000 inside the container with 3000 on current host

      docker run -p 3000:3000 -d dockerized-react


http://localhost:3000


Save the app through nginx:

nginx.conf

// nginx.conf


      server {
        listen 80;

        location / {
          root /usr/share/nginx/html/;
          include /etc/nginx/mime.types;
          try_files $uri $uri/ /index.html;
        }
      }


Dockerfile: 

      FROM node:16-alpine as builder

##### Set the working directory to /app inside the container

      WORKDIR /app
      
##### Copy app files

      COPY . .
      
##### Install dependencies (npm ci makes sure the exact versions in the lockfile gets installed)

      RUN npm ci 
      
##### Build the app

      RUN npm run build

##### Bundle static assets with nginx

      FROM nginx:1.21.0-alpine as production
      ENV NODE_ENV production
      
##### Copy built assets from `builder` image

      COPY --from=builder /app/build /usr/share/nginx/html
      
##### Add your nginx.conf

      COPY nginx.conf /etc/nginx/conf.d/default.conf
      
##### Expose port

      EXPOSE 80
      
##### Start nginx

      CMD ["nginx", "-g", "daemon off;"]

      docker build . -t dockerized-react

##### Notice we're now mapping port 80 inside the container 
##### to port 3000 on the host machine!

      docker run -p 3000:80 -d dockerized-react


===> End React App <======


----------------------------------------------------------

[Go To Top](#top)
## 3. 

##### ===> Angualr App <==========

Project Setup

Install the Angular CLI globally:

      npm install -g @angular/cli@7.3.10
      ng new angular-microservice 
      cd angular-microservice
      ng new angular-microservice –directory ./


Docker Setup:

Dockerfile

##### base image
      FROM node:12.2.0

##### set working directory
      WORKDIR /app
##### install and cache app dependencies
      COPY package.json /app/package.json
      RUN npm install
      RUN npm install -g @angular/cli@7.3.10

##### add app
      COPY . /app

##### start app
      CMD ng serve --host 0.0.0.0


      docker build -t angular-microservice:dev .

      docker run -d -v ${PWD}:/app -v /app/node_modules -p 4201:4200 --rm angular-microservice:dev

      docker run -d -v ${PWD}:/app -v /app/node_modules -p 4201:4200 --name foo --rm angular-microservice:dev


===> End Angular App <======
