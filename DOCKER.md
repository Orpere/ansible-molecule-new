# Create docker base image with systemd

## 1.create a image file

```zsh
# the entrypoint was wited for ubuntu 
 docker build -t [name] -f ./[dockerfile-distro] . 
```

## 2.run the image and test the systemd should work

```zsh
docker run -it --privileged  [name]  bash 
```

## 3.create a repo on docker hub

eg:  orlandop43/systemd-os:tagname

## 4.push the image to your docker hub repo

```zsh
docker tag local-image:tagname new-repo:tagname
docker push new-repo:tagname 
```
