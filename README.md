# Appdynamics-and-PCF-and-Python
A simple demo to instrument python flask Application using Appd python agent in PCF environment



### AppDynamics Python on Cloud Foundary

## Install and Setup

Step 1: Clone project and enter into project folder
```
git clone https://github.com/arungpro/Appdynamics-and-PCF-and-python.git
cd Appdynamics-and-PCF-and-Python/python-hello-world-flask
```
Edit: change appd.cfg file with your controller creds and details

Step 2: cf step and do login as define in https://docs.pivotal.io/partners/appdynamics/using.html

Step 3: Note: Python agent buildpack do not support cflinuxfs3 at this point. To fix this run
```
cf buildpacks | grep python
```
and choose something other as cflinuxfs3, that listed under the command output.

Step 4: Push to cloud with https://github.com/Appdynamics/python-buildpack as buildpack
```
cf push my-python-app -b https://github.com/Appdynamics/python-buildpack -s cflinuxfs2
```
Note: my-python-app is my pcf specific <app_name>.

Step 5: Create a user provided service to auto-discover the AppDynamics agent

        NOTE: Using cups based approach. One can use Appdynamics tiles, But its out of scope of this demo. 
 ```
cf create-user-provided-service appdynamics-python -p "host-name,port,ssl-enabled,account-name,account-access-key,application-name,tier-name,node-name"
 ```
 Enter details like hostname, port, Acc Name etc as added in Step 1.
 Note: If you are using Appdynamics tiles. You can skip this step.
 
Step 6: Bind the service with the app name
```
cf bind-service my-python-app appdynamics-python
```

Step 7: Restage after the Bind
```
cf restage my-python-app
```

Step 8: Run some continious load to the application for 10-15 mins and check in the controller UI to get controller relavent details
