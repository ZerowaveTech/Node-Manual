<p align="center">
    <img height="100" height="auto" src="https://user-images.githubusercontent.com/56349947/204550860-ecf49956-0283-4989-9b59-2469d7413ca7.svg">
</p>
<h1 align='center'>Docker Installation</h1>

## Update
```
sudo apt update && sudo apt upgrade -y
```
## Install Prerequisites Tools
```
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
sudo apt update && sudo apt install docker-ce docker-ce-cli containerd.io -y
```
## Get Docker Image
```
docker pull thepowerio/tpnode
```
## Run Docker
```
docker run -d -p 44000:44000 --name tptest thepowerio/tpnode
```

<h3 align='center'>Continue to step 2 send address to Rover Bot</h3>