# Welcome to my EE demo

> This demo was presented at Summit Connect in Utrecht, and aims to simiplify and explain the creation of Execution Environments.
> A Youtube Video where I execute the below steps are available here: <https://youtu.be/wecgEP3t5D0>

## Creating your EE

### Step 1 - Install Ansible Builder

- su - builder
- sudo dnf install python38-pip git podman; sudo dnf remove python36
- pip3 install --user ansible-builder; pip3 install --user ansible
- podman login registry.redhat.io
- podman pull registry.redhat.io/ansible-automation-platform-21/ee-minimal-rhel8:latest
- podman image list

### Step 2 - Create Build Directory and Definition Files

- cd ~; git clone https://github.com/HaaikeV/demo_ansible_create_ee.git; mv demo_ansible_create_ee ee_factory; cd ee_factory

### Step 3 - Populate The Definition Files Based On Your Collection Requirements

- execution-environment.yml = main file that includes the 3 files below.
- requirements.yml = put your collection here.
- requirements.txt = put you python/pip dependencies for your collection here.
- bindep.txt = put your DNF/YUM binaries here.

### Step 4 - Build

- ansible-builder build -f execution-environment.yml -t my-forti-ee:1.0 -v 2
- podman images #get image ID

### Step 5 - Push To An Image Repo

- podman login quay.io #you need an account
- podman push repo:version quay.io/hvanderm/repo:version

### Step 6 - Use The Image in AAP

- On the AAP menu (left hand side)
- Under "Administration"
- Click on Execution Environments and
- Click on "Add"

## Sources/References I used that might be interesting

- <https://access.redhat.com/documentation/en-us/red_hat_ansible_automation_platform/2.1/html/ansible_builder_guide/assembly-building-off-existing-ee>

- <https://ario.cloud/posts/ansible-builder-ee>

- <https://gregsowell.com/?p=7086>
