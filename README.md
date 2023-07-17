# Dockerized Python Flask "Hello World" Application in AWS EC2

This repository contains a simple Python Flask application which returns "Hello World" and the elapsed time since the application started. The application is designed to run within a Docker container. This repository demonstrate how to run this application in Amazon EC2.

## Files
The repository consists of the following files:
- `helloworld.py`: A Python script that runs a Flask web server. This server responds to requests on the root path (`/`) with a "Hello World from Python!" meesage and the time elapsed since the server started.
- `Dockerfile`: This file is used to create a Docker image that runs the Python script.

## Requirements
To run this application, you need:
- AWS EC2
- Python
- Docker

## How to Build and Run

### Creating AWS EC2
1. Launch an instance using your preferred Application and OS images, instance type and network settings.
2. Your security group should have inbound rules of SSH, HTTP and custom TCP with port range of 8080.
3. Launch EC2 instance connect
4. Run the following command to install `git` and `docker` in your EC2 instance.
    ```sh
    sudo su
    yum update -y
    yum install git -y
    yum install docker -y
    systemctl start docker
    ```
5. Run `systemctl status docker` to verify that the Docker service is active and running. Then, press the Q key to exit the pager and return to the command prompt.<br>
![ec2-docker-status](https://1drv.ms/i/s!Ap4RX7PG9du9gZNNKffzWOcoiNHymA?e=XaBLb2)

### Building the Docker Image
1. Clone this repository into your EC2 instance.
    ```sh
    git clone https://github.com/Dylon-Chan/python-helloworld-with-docker.git
    ```
2. Navigate to the directory containing the Dockerfile.
    ```sh
    cd python-helloworld-with-docker
    ```
3. Run the following command to build the Docker image with the repository name "helloworldapp". The `-t` flag tags the image and the `.` represents the current directory, which means that Docker will use the current directory and its contents as the build context. 
    ```sh
    docker build -t helloworldapp .
    ```
4. You can run the following command to list all images and you will see the `helloworldapp` image is built and its Image ID.
    ```sh
    docker image ls
    ```

### Running the Docker Container
Run the following command to start the Docker container. The `-d` allows the Docker container to run in the background, `-p 8080:8080` maps the port 8080 on your machine to port 8080 on the Docker container and lastly the command specifies to use `helloworldapp:latest` image.
```sh
docker run -d -p 8080:8080 helloworldapp:latest
```

### Testing the Application
1. You can run the following command to make a HTTP request to the access the web server.
    ```sh
    curl http://0.0.0.0:8080
    ```
2. Alternatively, you access the web server by navigating to the URL (http://<your-ec2-public-address>:8080) in your web browser.
    ```sh
    E.g: http://13.250.61.158:8080
    ```
Both methods allow you to see a message that says "Hello World from Python!" and the elapsed time since the server was started.
<br>
![helloworld-from-python](https://1drv.ms/i/s!Ap4RX7PG9du9gZNPDt6QAafrv5cyHA?e=lobbcE)