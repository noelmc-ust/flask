# Dockerization and Deployment of the Flask App

## Dockerfile
First we need to create the dockerfile for the app . since we are using a Flask Server our docker file should be like this

```
FROM python:3.9.2
WORKDIR /flask
COPY requirements.txt ./
RUN pip install -r requirements.txt
COPY . .
ENV FLASK_APP=app.py
EXPOSE 5000
CMD ["python", "-m", "flask", "run", "--host=0.0.0.0", "--port=5000"]
```

1. we are installing the python docker image
2. we set the working directory of our app
3. to install the dependency we copy the requirements.txt file into the working directory
4. running "pip install -r requirements.txt" to install the dependencies
5. copying our whole source code into the working directory
6. we set our app.py as FLASK_APP variable to tell flask which to run
7. we set our flask app to run at 5000 so we expose it
8. The CMD command make that sure the server is started and is available for everyone and our app is running at port 5000 


        Dont forget to add .dockerignore file to avoid unenecssary files while creating image

## Image and Container Creation

We clone our git repo into the EC2 instance and from there we go into the cloned repo and run the docker builc command to create image of that project
```
docker build -t <name> <location of docker file>
```
after sucessfully creating the image we need to create the container so we run the docker run command to crrate it in daemon mode (so app runs in background, dosent exit when we exit the container)

```
docker run -td --name <name of app> -p <host:3000> <image name>
```
```
http://13.127.6.204:82 - App is hosted in this link
```
after creating the container we need can check if the app is working the web

## Pushin the image into docker hub

First we need to tag our image 
```
docker tag <image name> <username/new image name>
```

after tagging it we push it into the docker hub
```
docker push <new image name>
(find it by running docker ps)
```
```
https://hub.docker.com/repository/docker/nmc9812/flask - docker image link
```

