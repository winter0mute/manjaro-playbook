# Manjaro/Arch Linux Ansible Provision

This is an Ansible playbook meant to provision a Manjaro or Antergos Linux distribution,
based on Arch Linux. It should run locally after a clean OS install.

## Preamble

1. Refresh the copy of the master package database from the server and install `Ansible` and `Git`.  
Also do a reboot to reload the newly installed packages/modules.
```
sudo pacman -Syyu --noconfirm
sudo pacman -S ansible git --noconfirm
sudo reboot
```

2. Git clone the current project
```
git clone https://github.com/winter0mute/manjaro-playbook.git
```

## Run

### Install everything
```
ansible-galaxy install -r requirements.yml
ansible-playbook playbook.yml --extra-vars="user_name=$(who | head -n1 | cut -d' ' -f1) user_email=EMAIL" --ask-become-pass
```

### Install everything with debug turned on
```
ansible-galaxy -v install -r requirements.yml
ansible-playbook -vvv playbook.yml --extra-vars="user_name=$(who | head -n1 | cut -d' ' -f1) user_email=EMAIL" --ask-become-pass
```

## Playbook Tags

Tags supported:

| Tag       | Description                                                             |
|-----------|-------------------------------------------------------------------------|
| base      | Install Linux util libraries, python-pip, terminator                    |
| browsers  | Install Chrome                                                          |
| dev-tools | Install Docker, jq                                                      |
| editors   | Install vim, atom, and gimp                                             |
| flatpak   | Install flatpak                                                         |
| aur       | Install Arch User Repository libraries                                  |

Example on how to install only browsers:
```
ansible-playbook playbook.yml --extra-vars="user_name=$(who | head -n1 | cut -d' ' -f1) user_email=EMAIL" --ask-become-pass --tags browsers
```

## TODO

Bluemix setup:
 * enable zsh completion, add the following line in "~/.zshrc":
   . /usr/local/ibmcloud/autocomplete/zsh_autocomplete
 * IBM Cloud CLI automatically collects data for usage analysis and user experience improvement. To disable the collecting, run "ibmcloud config --usage-stats-collect false"
 * IBM Cloud CLI has a plug-in framework to extend its capability. To install the recommended plug-ins and dependencies, run the install script from http://ibm.biz/install-idt. For additional plug-in details, see https://console.bluemix.net/docs/cli/reference/bluemix_cli/extend_cli.html.
 * Install the container-registry ibmcloud plugin install container-registry -r Bluemix
   Use 'ibmcloud plugin show container-registry' to show its details.
 * Install the kubernetes CLI tool (ibmcloud ks) : ibmcloud plugin install container-service
