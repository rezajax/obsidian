Social media
https://hub.docker.com 



```bash

// run 
sudo docker run hello-world

//list images 
sudo docker images

//Processes 
sudo docker ps

//Processes -a #archive
sudo docker ps -a

// busybox 
sudo docker run busybox echo "docker is fun .. at least useful"

```

## Remove

remove container (processes)
```bash
sudo docker ps -a
sudo docker rm CONTAINER_ID
```
Remove All container run before
```bash
sudo docker container prune
```

Remove Image
```bash
sudo docker images
sudo docker rmi IMAGE_NAME
```


## Auto Remove
```bash
sudo docker run --rm busybox
```

## Interactive and TTY

>[!help]
>-i, --interactive                      Keep STDIN open even if not attached
> -t, --tty                              Allocate a pseudo-TTY


```bash
sudo docker run --rm -it busybox
```

