## Example Use Cases for snyk in a Dockerfile
__1 - fail a `docker build` if snyk detects vulnerabilities | [Dockerfile.snyk_test](Dockerfile.snyk_test)__

Example invocation, pass $SNYK_TOKEN as a dynamic build argument to authenticate the CLI
```
docker build -t snyk-in-dockerfile:test \
             --build-arg snyk_token=${SNYK_TOKEN} \
             -f Dockerfile.snyk_test .
```
2. package snyk CLI into application container to test via `docker run`
3. instrument snyk test in a multi-stage docker build
