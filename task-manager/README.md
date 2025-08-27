# How to Push Docker image on DockerHub

### 1. Build the Docker image
	docker build -t <your-dockerhub-username>/task-manager:latest .
### 2. Test the image locally
	docker run -d -p 8080:80 --name <your-dockerhub-username>/task-manager:latest

Visit  [http://localhost:8080](http://localhost:8080/)  in your browser to test the application.

### 3. Push to Docker Hub
#### Log in to Docker Hub (if not already logged in)
	docker login
	use your PAT key (from DockerHub)

#### Push the image to Docker Hub
	docker push <your-dockerhub-username>/task-manager:latest