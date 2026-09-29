<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Deploy an App with Docker

**Project Link:** [View Project](https://nextwork.ai/projects/20d7108c-6f3a-54d8-aa67-310ae922191d)

**Author:** Abdul Hussein  
**Email:** abdulhussein@hotmail.se

---

![Image](https://nextwork.ai/authentic_blue_lucky_ferret/uploads/20d7108c-6f3a-54d8-aa67-310ae922191d_c4df13c84)

## Introducing Today's Project!

### What is Docker?

Docker is a platform for building, running, and sharing containers, which package an app together with everything it needs to run. It is useful because the app behaves the same on any machine, whether that's my laptop or a cloud server, and it avoids "it works on my machine" problems. It also keeps apps isolated from each other and makes them quick to start and easy to move around. I used Docker in this project to write a Dockerfile that starts from an Nginx image and adds my custom index.html, build that into an image, and run it as a container on my computer to see my webpage load in the browser. I then used that image to deploy the app with Elastic Beanstalk.

### One thing I didn't expect...

One thing I didn't expect in this project was getting an error when I ran my custom image. It turned out another container was already using port 80, and only one container can use a port on my computer at a time.

### This project took me...

This project took me approximately 45 min.

## Understanding Containers and Docker

### Containers

Containers are lightweight, isolated packages that bundle an application together with everything it needs to run: code, runtime, libraries, and configuration. Like shipping containers, they're standardized, so the app runs the same way wherever you put it, whether that's your laptop, a teammate's machine, or a cloud server. They're useful because they avoid "it works on my machine" problems, keep apps isolated from each other, start quickly, and make deploying and moving apps much easier.

A container image is a blueprint or template for making containers. It tells Docker exactly what to put inside each container - things like your app’s code, the libraries it needs, and any other required files.

### Docker

Docker is an open-source platform for building, running, and shipping containers. It gives you the tools to package an app and its dependencies into an image (using a Dockerfile), run that image as a container, and share images through registries like Docker Hub. It's the most widely used container technology, which is why "Docker" is often used as a synonym for "containers."

The Docker daemon is the engine that actually does the thing when you run Docker commands e.g. create a container.

## Running an Nginx Image

Nginx (pronounced “engine-x”) is a web server, which is a program you use to run websites and web apps. If you want people to visit your site, you're going to need a web server to deliver your website's files to their browsers.

The command I ran to start a new container was "docker run -d -p 80:80 nginx"

![Image](https://nextwork.ai/authentic_blue_lucky_ferret/uploads/20d7108c-6f3a-54d8-aa67-310ae922191d_6245f5bb10)

## Creating a Custom Image

A Dockerfile is a document with all the instructions for building your Docker image. Docker would read a Dockerfile to understand how to set up your application's environment and which software packages it should install.

My Dockerfile tells Docker three things. First, FROM nginx:latest says to start from the latest official Nginx image, so I don't have to build a web server from scratch and can just customize an existing one. Second, COPY index.html /usr/share/nginx/html/ replaces Nginx's default webpage with my own index.html file, so the server shows my content. Third, EXPOSE 80 says the container should receive web traffic on port 80, the standard port for web pages, which will matter when I connect to it from my browser in the next step.

The command I used to build a custom image with my Dockerfile was "docker build -t my-web-app ." The '.' at the end of the command tells Docker to find the Dockerfile in the current directory i.e. the Compute folder.

![Image](https://nextwork.ai/authentic_blue_lucky_ferret/uploads/20d7108c-6f3a-54d8-aa67-310ae922191d_4c741d1913)

## Running My Custom Image

There was an error when I ran my custom image because another container was already using port 80, so the new container couldn't bind to it. Only one container can use a given port on my computer at a time. I resolved this by stopping the container that was using port 80 (with docker stop, or by stopping it in Docker Desktop), and then running my custom image again, which could now claim the port.

In this example, the container image is the packaged template I built from my Dockerfile: Nginx plus my custom index.html, with port 80 exposed. It's a read-only blueprint that doesn't run on its own. The container is a running instance of that image, the live Nginx web server serving my webpage on my computer.

![Image](https://nextwork.ai/authentic_blue_lucky_ferret/uploads/20d7108c-6f3a-54d8-aa67-310ae922191d_74b5c3d619)

## Elastic Beanstalk

AWS Elastic Beanstalk is a service that makes it easy to deploy cloud applications without worrying about the underlying infrastructure.

Deploying my custom image with Elastic Beanstalk took me 3 minutes.

![Image](https://nextwork.ai/authentic_blue_lucky_ferret/uploads/20d7108c-6f3a-54d8-aa67-310ae922191d_26d5573b23)

## Deploying App Updates

---

*Built with [NextWork](https://nextwork.ai) - [View this project](https://nextwork.ai/projects/20d7108c-6f3a-54d8-aa67-310ae922191d)*
