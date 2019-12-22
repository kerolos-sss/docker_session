# our base image
FROM python:3-onbuild

# specify the port number the container should expose
EXPOSE 5000

COPY ./requirements.txt ./requirements.txt

RUN pip install -r requirements.txt

COPY . .

# run the application
CMD ["python", "./app.py"]