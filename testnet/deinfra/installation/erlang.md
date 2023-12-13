<p align="center">
    <img height="100" height="auto" src="https://user-images.githubusercontent.com/56349947/204550860-ecf49956-0283-4989-9b59-2469d7413ca7.svg">
</p>
<h1 align='center'>Erlang Installation Guide for Ubuntu 20.xx</h1>

## Add GPG Key
```
echo "deb https://packages.erlang-solutions.com/ubuntu focal contrib" | sudo tee /etc/apt/sources.list.d/erlang-solution.list
```
## Update Package
```
apt update && apt upgrade -y
```
## Install Erlang
```
apt install erlang
```