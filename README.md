dockingclamps
=============

Distributed cloud deployment for docker.io containers


Docking clamps are devices which allow two starships to connect together. Dockingclamps is a cloud deployment tool for configuring and deploying docker containers.  At its core dockingclamps consists of a distributed configuration database and a set of utilities for provisioning and deploying containers on virtual machines in an OpenStack environment.

Getting a Started
-----------------

In order to get a current build of dockingclamps running you can deploy using docker:

        docker pull cthulhuology/dockingclamps
        docker run -i -d -p 53:53 -p 5673:5673 -p 7600:7600 -t cthulhuology/dockingclamps

This will expose the DNS server, AMQP server, and the management interface on the public address of your management node. If you setup DNS for your management node as clamps.mydomain.com, You can then go to the web interface at http://clamps.mydomain.com:7600/ and setup your management account. 


Deploying a VM
--------------

After you setup your management account, you will need to setup a VM image suitable for use with dockingclamps. The easiest way to do this is to take a base Ubuntu 13.04 image and run the following command as root:

        \curl -L https://raw.github.com/cthulhuology/dockingclamps/bootstrap | DOCKINGSTATION=clamps.mydomain.com bash

This will install the necessary kernel modules, lxc containers, docker, and a set of utilities which will enable dockingclamps to manage the node.   The DOCKINGSTATION hostname will be baked into your image so that any node that is spun up from this VM image will automatically announce and configure itself with the management node.  Once you have finished the process, the VM will be imaged and the management node will use it for future deployments. 


Configuring a Deployment
------------------------

Dockingclamps uses an internal DNS server to provide configuration information for all of the nodes. As docker also supports passing environment variables to running containers, this becomes a convenient way to deploy configuration information in a scalable fashion. 
