# learn-cicd-starter (Notely)

![code coverage badge](https://github.com/GnarlyLasagna/learn-cicd-starter/actions/workflows/ci.yml/badge.svg)

This repo contains the starter code for the "Notely" application for the "Learn CICD" course on [Boot.dev](https://boot.dev).

## Local Development

Make sure you're on Go version 1.20+.

Create a `.env` file in the root of the project with the following contents:

```bash
PORT="8080"
```

Run the server:

```bash
go build -o notely && ./notely
```

- *This starts the server in non-database mode.* It will serve a simple webpage at `http://localhost:8080`.

- You do *not* need to set up a database or any interactivity on the webpage yet. Instructions for that will come later in the course!

install gosec with Go
```
go install github.com/securego/gosec/v2/cmd/gosec@latest
```

or install gosec with brew
```
brew install gosec
```

install staticcheck with Go
```
go install honnef.co/go/tools/cmd/staticcheck@latest
```

or install staticcheck with Brew
```
brew install gosec
```

Run the scripts/buildprod.sh script found in the root of the Notely repository. This will produce a notely binary that's compiled for Linux, which is the OS our Docker image will run on.
```
./scripts/buildprod.sh
```

Next, build the Docker image locally:
DOCKERHUB_NAMESPACE should be replaced with your Docker Hub username.
```
docker build -t DOCKERHUB_NAMESPACE/notely:latest .
```

Run the Docker image locally:
```
docker run -e PORT=8080 -p 8080:8080 DOCKERHUB_NAMESPACE/notely:latest
```
Open the app in your browser at http://localhost:8080. You should see the Notely app running locally!


GOOGLE CLOUD PLATFORM
GCP is one of the "big three" cloud providers, along with AWS and Azure. We're use GCP to host our Notely application!

GOOGLE CLOUD SDK
For some tasks, it makes sense to use the gcloud CLI instead of the GCP web console. For example, to run tasks from a GitHub Actions workflow, we'll need to use the gcloud CLI.

```
gcloud init
```

```
gcloud config list
```


