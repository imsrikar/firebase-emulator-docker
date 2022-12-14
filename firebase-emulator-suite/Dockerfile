# The base image is node:slim, which is a slim version of the Node.js runtime environment.
FROM node:slim

ADD . /app
WORKDIR /app

# Install OpenJDK-11

#Add the stretch-backports repository to the sources.list.d directory, using the echo and tee commands. This will allow you to install the Open JDK 11 runtime environment from the backports repository.
RUN echo 'deb http://ftp.debian.org/debian stretch-backports main' | tee /etc/apt/sources.list.d/stretch-backports.list

# Update the package list using the apt-get update command.
# Install the Open JDK 11 runtime environment using the apt-get install command.
# Clean up the container by removing unused packages and cleaning the package cache, using the apt-get autoremove and apt-get clean commands.
RUN apt-get update -y && \
    apt-get autoremove -y && \
    apt-get install -y openjdk-11-jre-headless && \
    apt-get clean;

#The RUN instruction is used to install the firebase-tools package globally using npm.
RUN npm i -g firebase-tools

# The RUN instruction is used to run the firebase --version command, which prints the version of the firebase-tools package.
RUN firebase --version

#The final step is to set the ENTRYPOINT for the container, which specifies the command to run when the container is started. 
#This command starts the firebase emulators with specific options for a project named "test-project" and exports and imports data from the ./data directory.
ENTRYPOINT ["firebase", "emulators:start","--project", "test-project", "--export-on-exit", "./data", "--import", "./data"]