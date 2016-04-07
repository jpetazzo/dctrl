dctrl
=====


Script to create a docker container helping with controlling a Docker engine from a Docker container.

Read [~jpetazzo/One container to rule them all](http://jpetazzo.github.io/2016/04/03/one-container-to-rule-them-all/) for more info.


Usage
-----

Create a data container named `purple`, holding the information necessary to connect to the current Docker API endpoint

    dctrl purple  
    

Then, if you need to run a container that has access to this Docker API endpoint, you can do:

    eval \$(docker run --rm --volumes-from $CONTROL alpine 
           sed 's/DOCKER_/DOCKERCONTROL_/' /docker/env)"

    docker run --volumes-from $CONTROL \
      -e DOCKER_HOST=\$DOCKERCONTROL_HOST \
      -e DOCKER_TLS_VERIFY=\$DOCKERCONTROL_TLS_VERIFY \
      -e DOCKER_CERT_PATH=\$DOCKERCONTROL_CERT_PATH \
      …

