# swagger-csharp


## Background

This repo was forked off of the CircleCI dockerfile-wizard repo.

The standard CircleCI docker images don't come with the tools needed by the `build_client_libs.sh` script in the oooh-swagger repo. 
Specifically mono. You also can't run root commands in the circleci config file, so things that can only be installed via root 
(like mono - eg `apt-get install -y mono-complete`) need to be added to a custom docker image that gets built with the circleci 
dockerfile-wizard. 

I forked the repo for this tool into this dockerfile-wizard repo and updated the circleci config to add the installation steps for the 
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

## Testing

Unfortunately, it seems the only way to really test this is to make changes and push to master so CircleCI builds it.  
Some basic testing can be done by loading the existing docker image as described above and try out the commands you want
to add to the Dockerfile. Once the .circleci/config.yml file has been updated with Docker RUN commands that you think work,
push the changes to master and wait for the CircleCI job (https://circleci.com/gh/ooohtv/dockerfile-wizard) to finish.  
Once it is done, check for the new image at https://cloud.docker.com/u/dhilder/repository/docker/dhilder/swagger-csharp. If  
it is there, update the .circleci/config.yml in the oooh-swagger repo to reference the new swagger-csharp tag and run
`./tools/circleci_local.sh generate-unity-client-libs` to see if the build works. If so, push the changes in the oooh-swagger repo.