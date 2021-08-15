## INSTALL MIRANTIS CONTAINER RUNTIME
```
sudo apt-get --yes remove docker docker-engine docker-ce docker-ce-cli docker.io
sudo apt-get --yes update
sudo apt-get --yes install apt-transport-https ca-certificates curl software-properties-common
DOCKER_EE_URL="http://repos.mirantis.com"
DOCKER_EE_VERSION=19.03
curl -fsSL "${DOCKER_EE_URL}/ubuntu/gpg" | sudo apt-key add -
sudo apt-key fingerprint 6D085F96
sudo add-apt-repository "deb [arch=$(dpkg --print-architecture)] $DOCKER_EE_URL/ubuntu $(lsb_release -cs) stable-$DOCKER_EE_VERSION"
sudo apt-get --yes update
sudo apt-get --yes install docker-ee docker-ee-cli containerd.io
```
## ADD DOCKER GROUP
```
sudo groupadd docker
sudo usermod -aG docker $USER
newgrp docker
docker run hello-world
```
## INSTALL MIRANTIS KUBERNETES ENGINE
```
docker container run --rm --interactive --tty --name ucp --volume /var/run/docker.sock:/var/run/docker.sock mirantis/ucp:3.4.4 install --host-address $( ip route | grep dev.eth0.proto.kernel | awk '{ print $9 }' ) --interactive --force-minimums
```