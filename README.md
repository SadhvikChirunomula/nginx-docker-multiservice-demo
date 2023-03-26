# Hosting Multiple Services and Exposing Them with Nginx

The Docker Compose file creates three services: `nginx`, `web1`, and `web2`.

- `nginx` is an Nginx reverse proxy that listens on port 1000 and forwards requests to the two web services.

- `web1` and `web2` are two separate web services, each serving a simple HTML page.

The `nginx` service is configured to forward requests to the `web1` and `web2` services based on the domain name in the `Host` header of the incoming HTTP request.

In the Docker Compose file, the `nginx` service is defined with a `ports` directive to publish port 1000 on the host machine, and a `volumes` directive to mount the Nginx configuration file (`nginx.conf`) from the host machine to the container. The `web1` and `web2` services are defined with a `build` directive that specifies the build context (directory containing the Dockerfile) and the Dockerfile path.

The Nginx configuration file (`nginx.conf`) specifies the domain names and corresponding web service addresses that Nginx should use to route incoming requests. In this example, the `server_name` directive specifies two domain names (`service1.example.com` and `service2.example.com`) and their corresponding web service addresses (`web1:8080` and `web2:8081`, respectively).

When a client sends an HTTP request to `nginx` on port 1000, Nginx examines the `Host` header to determine which web service to forward the request to. If the `Host` header is `service1.example.com`, Nginx forwards the request to the `web1` service on port 8080. If the `Host` header is `service2.example.com`, Nginx forwards the request to the `web2` service on port 8081.

To run this setup, you'll need to create two simple HTML pages (`index.html`), one for each web service, and save them in separate directories. The directories for `web1` and `web2` are specified in the Docker Compose file with the `build` directive.

To start the services, navigate to the directory containing the Docker Compose file and run the command `docker-compose up`. This will build the Docker images for the `web1` and `web2` services and start all three services (`nginx`, `web1`, and `web2`) in separate containers.

You can access the web services by navigating to `http://localhost:1000` in a web browser and specifying either `service1.example.com` or `service2.example.com` as the `Host` header in the HTTP request. Nginx will forward the request to the appropriate web service based on the `Host` header.
