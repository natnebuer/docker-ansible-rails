# README

## Getting Deployment Production Ready

### Building the ansible docker container

`docker build -t ansible:2.6.5 .`

### Before Running playbook

`apt install python`, ensure that python is installed in the remote machine

### Set up Database and Webservers

To configure server run :
```
docker run --rm -it \
  -v ~/.ssh/id_rsa:/root/.ssh/id_rsa \
  -v ~/.ssh/id_rsa.pub:/root/.ssh/id_rsa.pub \
  -v $(pwd)/deploy/production/ansible:/ansible/playbooks \
  ansible:2.6.5 setup.yml -i hosts
```

### Deployment to Production

```
docker run --rm -it \
  -v ~/.ssh/id_rsa:/root/.ssh/id_rsa \
  -v ~/.ssh/id_rsa.pub:/root/.ssh/id_rsa.pub \
  -v $(pwd)/deploy/production/ansible:/ansible/playbooks \
  ansible:2.6.5 deploy.yml -i hosts
```

### Troubleshoot

(Only if you are on Ubuntu 18.04 ) If you encounter issues with installed passenger, you can take a look at :

Please refer to this https://github.com/phusion/passenger/issues/2109 if you encounter an error installing passenger.