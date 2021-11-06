## Example use cases for snyk in a Dockerfile
__1 - [Dockerfile.snyk_test](Dockerfile.snyk_test) | fail a `docker build` if snyk detects vulnerabilities__

Example docker build invocation, passing $SNYK_TOKEN as a dynamic build argument to authenticate the CLI
```
docker build -t snyk-in-dockerfile:test \
             --build-arg snyk_token=${SNYK_TOKEN} \
             -f Dockerfile.snyk_test .
```

See [Github Workflow example](/actions/workflows/snyk_test.yml)

__2 - [Dockerfile.snyk_run](Dockerfile.snyk_run) | package snyk CLI into application container to test later via `docker run`__

First build the application with snyk included in the resulting image
```
docker build -t snyk-in-dockerfile:run \
             -f Dockerfile.snyk_run .
```
Invoke snyk security test via `docker run`
```
docker run -it --rm -e SNYK_TOKEN \
           snyk-in-dockerfile:run \
           snyk test --json
```

__3 - [Dockerfile.snyk_multistage](Dockerfile.snyk_multistage) | instrument snyk test in a multi-stage docker build__

First build the target stage which includes both snyk and the application
```
docker build -t snyk-in-dockerfile:multistage \
             -f Dockerfile.snyk_multistage \
             --target snyk .
```
Invoke the snyk security test via `docker run`
```
docker run -it --rm  -e SNYK_TOKEN \
           snyk-in-dockerfile:multistage
```
