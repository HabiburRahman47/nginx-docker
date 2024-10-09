# NGINX BASIC WITH DOCKER and DOCKER COMPOSE
This project sets up an Nginx server with Docker and Docker Compose. It serves custom HTML files and uses a custom configuration ('nginx.conf').
The configuration is mounted from the host system to the container, allowing you to manage your web server and content easily.

## Project structure

```
.
├── Dockerfile
├── README.md
├── docker-compose.yml
├── html
│   ├── fruits
│   │   └── demo.html
│   ├── index.html
│   └── other
│       ├── demo.html
│       └── index.html
├── nginx
│   └── nginx.conf
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
    a. Clone this project
    ```bash
    git clone https://github.com/HabiburRahman47/nginx-docker.git
    cd nginx-docker
    ```
    b. Start the Docker container
    ```bash
    docker-compose up -d
    ```   
   
3. Access the Web Application
    After starting the container, open a web browser and visit the following URLs:
    - http://localhost:8080/ : Displays the index.html file from the html directoroy.
    - http://localhost:8080/fruits/ : Displays the demo.html file from the html/fruits directory.
    - http://localhost:8080/other/ : Displays the index.html file from the html/other directory.


## Customization
### Updating Configuration or HTML files
a. Make your changes to the `nginx.conf` file or the HTML files in the `./html` directory.
b. Restart the Nginx service to apply the changes
```bash
docker-compose restart nginx-docker
```
### Making Changes Requiring a Rebuild
If you've made changes to the Dockerfile or need to rebuild the container for any reason:
a. Stop the containers:
```bash
docker-compose down
```
b. Rebuild the containers:
```bash
docker-compose build
```
c. Start the containers again:
```bash
docker-compose up -d
```

## Viewing Logs
To view the logs of your containers:
```bash
docker-compose logs
```
Add the -f flag to follow the logs in real-time:
```bash
docker-compose logs -f
```    

## Conclution
    This project demonstrates how to run an enginx server using Docker with custom configuration and HTML files. By mounting the nginx.conf and html directory from the host, you can easily update your web server setup.

## License
    MIT