# car-park

## Build docker image and run

1. Execute command below to build a Docker image
```console
docker build -t carpark .    
```

2. Execute command below to run the app in a Docker container
```console
docker run -it -p 8080:80 --rm --name carpark-1 carpark    
```

You should now be able to access the app on `localhost:8080`.
