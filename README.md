## Assisted Installer API Python Client Generator

Scripts to generate the python client for the Assisted Service API (https://github.com/openshift/assisted-service).

Requirements:
- curl
- jq
- docker/podman container runtime (optional)


The ```generator.sh``` script, by default, uses the online generator found at http://api.openapi-generator.tech to create 
the python client for the latest version of the Assisted Service API within the ```assisted-service-client-python-master``` directory.
```
# Generate the python client from the master branch
./generate.sh
```

It's also possible to generate the client for a specific verson:
```
ASSISTED_SERVICE_VERSION=v1.0.19.2 ./generate.sh
```

Or use the swagger online generator service instead:
```
OPENAPI_GENERATOR_URL=https://generator.swagger.io ./generate.sh
```

It's also possible use a local generator by running the ```generate-from-local-container.sh``` script.
A container runtime (docker or podman) is needed in this case.

The default execution uses docker to run the **openapitools/openapi-generator-online** container image and maps the '8888' port to the container
```
./generate-from-local-container.sh
```

It's possible to use podman instead of docker:
```
CONTAINER_RUNTIME_COMMAND=podman ./generate-from-local-container.sh
```

Or change the local port mapped to the container:
```
OPENAPI_GENERATOR_PORT=8080 ./generate-from-local-container.sh
```

It's also possible to use the swagger generator image:
```
OPENAPI_GENERATOR_IMAGE=swaggerapi/swagger-generator ./generate-from-local-container.sh
```

All the commands above will create a new directory ```assisted-service-client-python-${ASSISTED_SERVICE_VERSION}```
containing the python client code: 
```
ASSISTED_SERVICE_VERSION=v1.0.19.2
./generate.sh
cd assisted-service-client-python-${ASSISTED_SERVICE_VERSION}
python setup.py install --user
```