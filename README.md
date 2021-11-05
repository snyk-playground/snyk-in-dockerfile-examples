## Example Use Cases for snyk in a Dockerfile
__1 - [Dockerfile.snyk_test](Dockerfile.snyk_test) | fail a `docker build` if snyk detects vulnerabilities__

Example docker build invocation, passing $SNYK_TOKEN as a dynamic build argument to authenticate the CLI
```
docker build -t snyk-in-dockerfile:test \
             --build-arg snyk_token=${SNYK_TOKEN} \
             -f Dockerfile.snyk_test .
```
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
           snyk test
```

3. instrument snyk test in a multi-stage docker build
