# Appdynamics-and-PCF-and-Python
A simple demo to instrument python flask Application using Appd python agent in PCF environment



### AppDynamics Python on Cloud Foundary

## Install and Setup

Step 1: Clone project and enter into project folder
```
git clone https://github.com/arungpro/appdynamics-python-docker-sample.git
cd appdynamics-python-docker-sample
```

Step 2: Edit appd.cfg file with your controller creds and details

Step 3: Build the Docker image
```
docker build -t python-docker:v1 .
```

Step 4: Start the container
```
docker run -p 5000:5000 python-docker:v1
```

Step 5: Drive continuous load to the application
```
http://localhost:5000/
```

