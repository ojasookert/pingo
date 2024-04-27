# Introduction

This is an exercise to test your skills. You will be going through the process of setting up a VM with a service that mimics the behaviour of the real thing. You can then go through the official workplan with this service ask questions along the way if you get stuck.

The main goal is to replace the vulnerable Pingo web application with a dockerized, patched version that sits behind a WAF.

# Setup

## Gamenet VM Setup

1. Install VMware Workstation Player
2. Download [Pingo VM](https://drive.google.com/file/d/1PLyp5MjO8pxd-W7vrnecoVEclezzlQBr/view?usp=drive_link)
3. Import the OVF to VMWare Workstation Player
4. Start the VM
5. Login to VM with `root:Admin1Admin1`
6. Run `ip a` and check IP of `ens33`
7. Add this IP to your host machine's `/etc/hosts` file as `<ip-address> pingo.example.com`
8. Test access to the application in your host machine's browser by navigating to [http://pingo.example.com](http://pingo.example.com).

## Scoringbot Setup

1. Install Docker or Docker Desktop on your host machine
3. Run `docker run --rm -it --network=host ghcr.io/ojasookert/pingo-scoringbot:main`

# Workplan

## 1. Dump the application files locally

This can be done using scp or rsync. Make backups of all the VMs files locally in your host machine. This may or may not include web application code files, any proxy configurations, database dump and configuration, etc.

Note: Once you are sure you have backed up all necessary files, shut the VM down. If you need to access the VM again before step 7, you have failed step 1!

## 2. Set the application up locally

This means you should be able to change the IP address in your `/etc/hosts` file to `127.0.0.1` and run the scoringbot to achieve 100% result in tests.

## 3. Dockerize the application

This can be done as part of the previous step, but the goal is to have a single docker-compose.yml file that brings up the whole application and retains functionality so that scoringbot's tests pass.

## 4. Patch the local version of the application

This means you should investigate the application throroughly and patch any found vulnerabilities while documenting found issues and applied mitigations.

## 5. Enable Web Application Firewall

TODO

## 6. Re-tag and upload container images to your favourite Docker registry

TODO

## 7. Automate deployment

You should then create bash or ansible automation that targets the Pingo VM, replacing the original vulnerable application and related services with the containerized version with WAF included. The result of the scripts is that the Pingo VM should be able to pass all scoringbot tests and all vulnerability tests (not yet included in scoringbot). This step should be repeated to ensure a clean run and minimal downtime of the application.
