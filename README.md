# my .nixpkgs repository

This repository contains my .nixpkgs to setup and restore my configuration using nix-darwin.

### Prerequisites 

Since not all required packages are available via nixpkgs some are installed via brew beforehand.

```shell
brew install --cask iterm2
brew install awscli awsume
```

### Install nix, nix-darwin & home-manager channel

```shell
# install nix
sh <(curl -L https://nixos.org/nix/install)

nix-channel --add https://github.com/nix-community/home-manager/archive/master.tar.gz home-manager
nix-channel --add https://nixos.org/channels/nixpkgs-unstable unstable
nix-channel --update

# let nix-darwin handle /etc/nix/nix.conf
sudo mv /etc/nix/nix.conf /etc/nix/.nix-darwin.bkp.nix.conf

# install nix-darwin
nix-build https://github.com/LnL7/nix-darwin/archive/master.tar.gz -A installer
./result/bin/darwin-installer
```

### Clone this repository

```shell
rm -rf ~/.nixpkgs/
git clone https://github.com/f0x7C0/.nixpkgs.git ~/.nixpkgs/
```

### Apply nix-darwin configuration

```shell
darwin-rebuild switch
```

### Decrypt secrets

The secrets are en- / decrypted using GPG, which should be installed by now

```shell
git-crypt unlock
```

