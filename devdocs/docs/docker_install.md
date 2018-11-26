## Instal·lació Docker

### Ubuntu 18.04

Elimina versions anteriors:

`sudo apt-get remove docker docker-engine docker.io`

Actualitza repositoris i paquets:

`sudo apt-get update`
`sudo apt-get upgrade`

Dependencies necessaries:

`sudo apt-get install \`

`apt-transport-https \`

`ca-certificates \`

`curl \`

`software-properties-common`

`sudo apt-key fingerprint 0EBFCD88`

Afegeix repositoris:

`sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"`

Instal·lació:

`sudo apt-get install docker-ce`

Comprobació:

`sudo docker run hello-world`


## Instal·lació Portainer

### Ubuntu 18.04



```
$ docker volume create portainer_data
$ docker run -d -p 9000:9000 -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer

```

