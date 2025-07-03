
```bash

# Two months behind 0.9.0
# https://launchpad.net/~ppa-verse/+archive/ubuntu/neovim
sudo add-apt-repository ppa:neovim-ppa/stable
sudo apt update
sudo apt install neovim


# TarBall
curl -LO https://github.com/neovim/neovim/releases/latest/download/nvim-linux-x86_64.tar.gz
tar xzvf nvim-linux-x86_64.tar.gz
sudo mv nvim-linux-x86_64 /opt/nvim
sudo ln -s /opt/nvim/bin/nvim /usr/local/bin/nvim
nvim --version


```