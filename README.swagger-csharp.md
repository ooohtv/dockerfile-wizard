# swagger-csharp


## Background

This repo was forked off of the CircleCI dockerfile-wizard repo.

The standard ciricleci docker images don't come with the tools needed by the `build_client_libs.sh` script in the oooh-swagger repo. 
Specifically mono. You also can't run root commands in the circleci config file, so things that can only be installed via root 
(like mono - eg `apt-get install -y mono-complete`) need to be added to a custom docker image that gets built with the circleci 
dockerfile-wizard. 

I forked the repo for this tool into our own dockerfile-wizard repo and updated the circleci config to add the installation steps for the 
required tools to the dockerfile the wizard will use to create a new image.

The dockerfile-wizard circleci job then builds the image and pushes it to the configured repo (currently set to be my public dockerhub 
repo)

## Debugging

```
$ docker images
```

Get the image id of the dhilder/swagger-csharp image.

```
$ docker run -it IMAGE_ID /bin/bash
# mono --version
# apt intall -y mono
```
