# NGINX BASIC WITH DOCKER
This project sets up an Nginx server with Docker. It serves custom HTML files and uses a custom configuration ('nginx.conf').
The configuration is mounted from the host system to the container, allowing you to manage your web server and content easily.

## Project structure

```
.
├── Dockerfile
├── README.md
├── html
│   ├── fruits
│   │   └── demo.html
│   ├── index.html
│   └── other
│       ├── demo.html
│       └── index.html
└── nginx
    └── nginx.conf

```
## Nginx Configuration
```nginx
events{ }
http {
    server {
        listen 80

        # Root location (http://localhost/)
        location / {
            root /usr/share/nginx/html;
            index index.html;
        }

        # Fruits locaiton (http://localhost/fruits/)
        location /fruits/ {
            root /usr/share/nginx/html;
            index demo.html;
        }
        
        # Other location (http://localhost/other)
        location /other/ {
            root /usr/share/nginx/html;
            index index.html 404;
        }
    }
}

```
## Running the project with Docker
Follow these steps to run the Nginx server with Docker:

1. Ensure Docker is installed

    Make sure Docker is intalled on your system. You can install it from [Docker's official site](https://docs.docker.com/engine/install/)

2. Run the Nginx Container

    Run the following command to start the Nginx container with the custom configuration and HTML files: 
    
    ```bash
        docker run -d \
        --name nginx-docker-container \
        -p 8080:80 \
        -v $(pwd)/nginx/nginx.conf:/etc/nginx/nginx.conf:ro \
        -v $(pwd)/html:/usr/share/nginx/html:ro \
        nginx

    ```
3. Access the Web Application
    After starting the container, open a web browser and visit the following URLs:
    - http://localhost:8080/ : Displays the index.html file from the html directoroy.
    - http://localhost:8080/fruits/ : Displays the demo.html file from the html/fruits directory.
    - http://localhost:8080/other/ : Displays the index.html file from the html/other directory.

4. Stop and Remove the Container
    To stop the container, run:
    ```bash
    docker stop nginx-docker-container
    ```
    To remove the container, run:
    ```bash
    docker rm nginx-docker-container
    ```

## Troubleshooting
- If changes to nginx.conf are not reflected, reload the Nginx configuration inside the container:
    ```bash
    docker exec -it nginx-docker-container nginx -s reload
    ```
- If you can't access the application, ensure that the container is running:
    ```bash
    docker ps
    ```

## Conclution
    This project demonstrates how to run an enginx server using Docker with custom configuration and HTML files. By mounting the nginx.conf and html directory from the host, you can easily update your web server setup.

## License
    MIT