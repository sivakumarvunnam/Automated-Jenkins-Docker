# Automated-Jenkins-Docker

The Compose file is very straightforward. If defines only one service (main) and uses the newly built image. It is exposing ports 8080 for the UI and 50000 for the agents. Finally, it defines jenkins-user and jenkins-pass secrets.

We should create the secrets before deploying the stack. The commands that follow will use admin as both the username and the password.Feel free to change it to something less obvious.

           echo "admin" | docker secret create jenkins-user -
 
           echo "admin" | docker secret create jenkins-pass -

Now we are ready to deploy the stack.


           docker stack deploy -c jenkins.yml jenkins

A few moments later, the service will be up and running. Please confirm the status by executing 
           
           docker stack ps jenkins.

Let’s confirm that everything works as expected.

           open  "http://localhost:8080"

You’ll notice that this time, we did not have to go through the Setup Wizard steps. Everything is automated and the service is ready for use. Feel free to log in and confirm that the user you specified is indeed created.

If you create this service in a demo environment (e.g. your laptop) now is the time to remove it and free your resources for something else. The image you just built should be ready for production.

           docker stack rm jenkins
 
           docker secret rm jenkins-user
 
           docker secret rm jenkins-pass
