# Create docker base image with systemd

1.create a image file

```zsh
# the entrypoint was wited for ubuntu 
 docker build -t [name] . 
```

2.run the image and test the systemd should work

```zsh
docker run -it --privileged  [name]  bash 
```
