## Example use cases for snyk in a Dockerfile

__1 - [Dockerfile.snyk_multistage](Dockerfile.snyk_multistage) | instrument snyk test in a multi-stage docker build__

First build the target stage which includes both snyk and the application
```
docker build -t snyk-in-dockerfile:multistage \
             -f Dockerfile.snyk_multistage \
             --target builder-with-snyk .
```
Invoke the snyk security test via `docker run`
```
docker run --rm  -e SNYK_TOKEN \
           snyk-in-dockerfile:multistage snyk test
```

See [Github Workflow example](https://github.com/snyk-playground/snyk-in-dockerfile-examples/actions/workflows/snyk_multistage.yml)
