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

PLANETSCALE
PlanetScale is a cloud provider that specializes in hosting serverless MySQL databases. It's a great fit for Notely because it has a very generous free Hobby tier, and it's easy to use. It will require you to add a card, but you will not be charged unless you create a Scaler or Scaler Pro database.

PlanetScale runs on top of AWS/GCP infrastructure, so it's easy to keep latency low between our Cloud Run service and our database.


install the MySQL driver:
```
go get -u github.com/go-sql-driver/mysql
```

Next, you can install GoDotEnv for accessing your database credentials:
```
go get -u github.com/joho/godotenv
```

install planetscale cli
```
brew install planetscale/tap/pscale
```

authorize login
```
pscale auth login
```

enter shell for PLANETSCALE
```
pscale shell notely-db main
```

To make sure the database is working, run the following queries:
check version in the shell 
```
SELECT @@version;
```

create test table
```
CREATE TABLE test (
  id INT,
  name TEXT
);
```

show the table, then drop it for testing
```
SHOW TABLES;
```
```
DROP TABLE test;
```

Run the migrations
```
./scripts/migrateup.sh
```

SHOW TABLES; in the shell should now show the newly created table


# RECAP OF YOUR ACCOMPLISHMENTS:
- You set up a continuous integration pipeline with GitHub Actions that ensures new PRs pass certain checks before they are merged to main:
Unit tests pass
    - Formatting checks pass
    - Linting checks pass
    - Security checks pass

- You configured a cloud-based MySQL database hosted on PlanetScale
- You set up a continuous deployment pipeline with GitHub Actions that does the following whenever changes are merged into main:
    - Builds a new server binary
    - Builds a new Docker image for the server
    - Pushes the Docker image to the Google Artifact Registry
    - Deploys a new Cloud Run revision with the new image and serves the app to the public internet
Pat yourself on the back! That's a pretty robust setup for our simple CRUD app.

# SOME THINGS TO KEEP IN MIND
- GCP is just one of the 3 major cloud providers. AWS and Azure are also popular choices. In many ways, their offerings are similar, but sometimes the differences matter.
- Cloud Run handles a lot of complexity for you. Managing DNS, SSL, load balancing, and auto-scaling are all things that many companies do manually, so those are still useful skills to have, but are outside the scope of this course.
- PlanetScale is a fully-managed third-party database host. There are many options out there for databases and database hosting that are worth learning about, but again, outside the scope of this course.
- Essentially every technology/product we used in this course has viable alternatives. You don't need to know how to use all of them before your first job, but you should understand some of them.
