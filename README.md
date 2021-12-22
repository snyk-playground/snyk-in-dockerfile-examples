## Example use cases for snyk in a Dockerfile

__1 - instrument snyk test in a multi-stage docker build__

uses: [Dockerfile.snyk_multistage](Dockerfile.snyk_multistage)

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

__2 -  instrument snyk test using separate dockerfiles__

uses: [Dockerfile.build](Dockerfile.build) 
      [Dockerfile.build_snyk](Dockerfile.build_snyk) 

First build application using its builder base image
```
docker build -t myapp:build -f Dockerfile.build .
```

Build a new container image from the previous one, this time including snyk CLI
```
docker build -t myapp:build_snyk -f Dockerfile.build_snyk .
```

Invoke the snyk security test via `docker run`
```
docker run --rm -e SNYK_TOKEN myapp:build_snyk snyk test
```

See [Github Workflow example](https://github.com/snyk-playground/snyk-in-dockerfile-examples/actions/workflows/snyk_separate_dockerfiles.yml)
