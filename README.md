# hello_world
Creating a hello-world python program and dockerizing it

## Creating a hello-world program

First we have to create simple python Hello-world program.
The program is as follows:
````
from flask import Flask 
app = Flask(__name__) 

@app.route('/') 
def hello(): 
	return "welcome to the flask tutorials"


if __name__ == "__main__": 
	app.run(host ='0.0.0.0', port = 5001, debug = True) 

````
Save this program with name demo.py


## Dockerizing the Python file
 For dockerizing you need 
-Dockerfile and Requiremnts
 
Below is Dockerfile instruction set

````FROM python:alpine3.7 
COPY . /app
WORKDIR /app
RUN pip install -r requirements.txt 
EXPOSE 5001 
ENTRYPOINT [ "python" ] 
CMD [ "demo.py" ] 
````

Below is the requirements.txt instruction

````# requirements.txt file
flask
````

The above structure should look as :
````
python_demo
    ├── requirements.txt
    ├── Dockerfile
    └── demo
        └── demo.py
````

Now as we have our Dockerfile ready we are ready to build our Docker image. To build a docker image from Dockerfile use the below command:

```` 
docker build --tag python_demo .  
````

The docker image is build now. You can see it using "docker images" command

````
REPOSITORY                    TAG       IMAGE ID       CREATED          SIZE
python_demo                   latest    0bb4dbaf8811   41 seconds ago   91.6MB
````

Now to run the file on our host machine, we have to allocate specific port to the Docker images. The port are allocated using below cammand:

````
PS C:\Users\Neeraj Shukla\Desktop\python_demo> docker run --name python_demo -p 5001:5001 python_demo

````
Port 5001 is alloted for python_demo docker image. Now open yoour default browser and check if the program is running correctly. The webpage must look as below.


![docker_port](https://user-images.githubusercontent.com/79436509/114925076-45c25980-9e4c-11eb-815a-58e62ce1cec8.JPG)

Thus you have successfully build a docker images and alloted port to it.
