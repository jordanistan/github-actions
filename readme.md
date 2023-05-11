Sure, here's an example README.md file to explain how to run the Github Action:

# Docker Build and Push Github Action

This Github Action builds and pushes a Docker image to a container registry.

## Usage

To use this Github Action in your workflow, add the following code to your `.github/workflows/main.yml` file:

```yaml
name: Docker Build and Push

on:
  push:
    branches:
      - main

jobs:
  build-and-push:
    runs-on: ubuntu-latest
    steps:
    - uses: actions/checkout@v2
      
    - name: Login to Docker Hub
      uses: docker/login-action@v1
      with:
        username: ${{ secrets.DOCKER_USERNAME }}
        password: ${{ secrets.DOCKER_PASSWORD }}
      
    - name: Build Docker image
      run: docker build -t my-dockerhub-username/my-image:latest .
      
    - name: Push Docker image
      run: docker push my-dockerhub-username/my-image:latest
```

This Github Action performs the following steps:
1. Listens for pushes to the `main` branch of the repository.
2. Sets up a job to run on an Ubuntu machine.
3. Checks out the code from the repository.
4. Logs in to the container registry (Docker Hub in this case) using the `docker/login-action` Github Action.
5. Builds the Docker image using the `docker build` command and tags it with the desired repository and tag.
6. Pushes the Docker image to the container registry using the `docker push` command.

To use this Github Action, you'll need to:
- Replace `my-dockerhub-username/my-image` with the name of your Docker image and tag.
- Set up `DOCKER_USERNAME` and `DOCKER_PASSWORD` secrets in your Github repository to authenticate with Docker Hub.

You can customize this Github Action to suit your needs, such as by using a different container registry, adding additional build steps, or triggering the action on different branches or events.

## License

This Github Action is released under the [MIT License](LICENSE).