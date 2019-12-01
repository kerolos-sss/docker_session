Docker file
```
# our base image
FROM python:3-onbuild

# specify the port number the container should expose
EXPOSE 5000

# run the application
CMD ["python", "./app.py"]
```

building your own image

```
docker build -t kerolos/catnip2 .
```

giving the image a tag "kerolos/catnip2"


```
docker run -p 8888:5000 kerolos/catnip2
```


```
docker images
```


put it online
```
docker push yourusername/catnip2
```


access 

```
docker login
```


