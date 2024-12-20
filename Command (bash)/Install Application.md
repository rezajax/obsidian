# Docker


Run the following command to **uninstall** all conflicting packages:

```bash
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
```

Set up Docker's `apt` repository.

```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

Reza For linux mint use this:

> UBUNTU_CODENAME in mint pass ubuntu name

```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$UBUNTU_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

To install the latest version, run:

```bash
 sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
Verify that the installation is successful by running the `hello-world` image:

```console
 sudo docker run hello-world
```

> [!TIP] Receiving errors when trying to run without root?
> 
> The `docker` user group exists but contains no users, which is why you’re required to use `sudo` to run Docker commands. Continue to [Linux postinstall](https://docs.docker.com/engine/install/linux-postinstall) to allow non-privileged users to run Docker commands and for other optional configuration steps.

To create the `docker` group and add your user:

1. Create the `docker` group.

```bash
sudo groupadd docker
```

2. Add your user to the `docker` group.

```bash
sudo usermod -aG docker $USER
```

3. **Log out and log back** in so that your group membership is re-evaluated.

> If you're running Linux in a virtual machine, it may be necessary to restart the virtual machine for changes to take effect.

You can also run the following command to activate the changes to groups:

```bash
newgrp docker
```


---

sudo apt install google-android-platform-tools-installer


---

## Eclipse Temurin Package Names

The following name schema is being used:

## Deb installation on Debian or Ubuntu

1. Ensure the necessary packages are present:

```bash
apt install -y wget apt-transport-https gpg
```

2. Download the Eclipse Adoptium GPG key:

```bash
wget -qO - https://packages.adoptium.net/artifactory/api/gpg/key/public | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/adoptium.gpg > /dev/null
```

3. Configure the Eclipse Adoptium apt repository. To check the full list of versions supported take a look at the list in the tree at [https://packages.adoptium.net/ui/native/deb/dists/](https://packages.adoptium.net/ui/native/deb/dists/).

```bash
echo "deb https://packages.adoptium.net/artifactory/deb $(awk -F= '/^VERSION_CODENAME/{print$2}' /etc/os-release) main" | sudo tee /etc/apt/sources.list.d/adoptium.list
```

> [!NOTE]
> For Linux Mint (based on Ubuntu) you have to replace `VERSION_CODENAME` with `UBUNTU_CODENAME`.

```bash
sudo echo "deb https://packages.adoptium.net/artifactory/deb $(awk -F= '/^UBUNTU_CODENAME/{print$2}' /etc/os-release) main" | sudo tee /etc/apt/sources.list.d/adoptium.list
```

4. Install the Temurin version you require:

```bash
apt update # update if you haven't already
apt install temurin-17-jdk
```
