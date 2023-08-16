# Install NVIDIA GPU on an EC2 instance with Ubuntu Server 22.04

Update and Upgrade the System:
```
sudo apt update && sudo apt upgrade -y
Ensure the Latest CUDA is Installed:
```
This will automatically install the compatible NVIDIA driver:
```
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-keyring_1.1-1_all.deb
sudo dpkg -i cuda-keyring_1.1-1_all.deb
sudo apt-get update
sudo apt-get -y install cuda
```
Install Docker:

Add Docker's official GPG key and set up the Docker stable repository:
```
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt update
```
Install Docker CE:
```
sudo apt install -y docker-ce
```
Add your user to the Docker group to allow non-root access (you'll need to log out and back in or start a new session for this to take effect):
```
sudo usermod -aG docker $USER
```
Install NVIDIA Container Toolkit:

Set up the NVIDIA Docker repository and GPG key:
```
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -
curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
sudo apt update
```
Install the NVIDIA Container Toolkit:

```
sudo apt install -y nvidia-container-toolkit
```
Restart Docker to apply changes:

```
sudo systemctl restart docker
```
