# android-jenkins-docker
Docker image with Jenkins that can build Android apps.

# Building the image
Run the command
>docker build -t android-jenkins .

# Run the image
Run the command
>docker run --name android-jenkins -p 8080:8080 -p 50000:50000 -v SOME_HOST_PATH:/var/jenkins_home android-jenkins

Replace ```SOME_HOST_PATH``` with the path to a folder on your host system where you want Jenkins to store its builds and configurations, for example ```/var/android_jenkins_home``` on Linux systems. If port 8080 is already used by another process on your host, you can modify which port redirects to Jenkins. If you want Jenkins to be accessible on port 8090 on your host, then replace the port argument with ```8090:8080``` in the run command.

## Windows tips
Setting the host path for ```jenkins_home``` is a bit tricky on Windows hosts. First of all, you probably need to share the drive where the folder lives and [this resource explains how](https://rominirani.com/docker-on-windows-mounting-host-directories-d96f3f056a2c#.7ec1d330n). Then, you need to provide the path with forward slashes, for example ```c:/Users/myuser/android_jenkins_home:/var/jenkins_home```

# Accessing Jenkins
Point your browser to http://localhost:8080 (or whichever port you bound) and configure your build.

## Gradle tips
If you are using gradle to build your project, you will want to configure the build to use the gradle wrapper. If you just want to create apks, then set the task to ```assembleDebug``` or ```assembleRelease```. Finally, add ```-x lint``` to the switches section to avoid lint from creating errors and disrupting the build.

# Modifying the image
Just modify the Dockerfile in case you want to modify the environment, for example
* Android SDK version
* Buildtools version
* Jenkins plugins

PRs are welcome for example for simplifying the mechanism for installing multiple buildtools versions.
