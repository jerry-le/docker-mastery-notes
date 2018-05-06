# Docker editions

- Learn about the various editions of Docker
- Learn which to use on this course
- Learn Docker CE vs EE
- Learn Stable vs Edge releases

## Getting started
- Docker CE is Community Edition (free). Dokcer EE is Enterprise Edition (paid, supporting)
- Three major types of installs: Direct, Mac/Win, Cloud
	- Direct: Until 2016, mostly direct OS supported docker to run on its kernel is Linux. Now, there are more and more platforms support Docker natively like: Window Server 2016, RaspberryPi,...
	- Mac/Win: In MacOS or Window 10, Docker need to run in a virtual machine. It's a tiny [Linux Apline](https://alpinelinux.org/) (5Mb).
	- Cloud: AWS/Azure/Google

## Stable vs Edge
- Edge is process to release new version every month
- Stable is process to release new version every half of year. 

## Installation

#### Install on Linux
- There are 3 ways to install: script, store, docker-machine
	- script: latest Edge release
	- store: download from `store.docker.com`
	- docker-machine: 
	- Don't use pre-installed setups (Digital Ocean, Linode, etc)

#### Install on Mac
- To use docker, Mac should be produced after 2010. Because, only after 2010, Macbook support Hypervisor. The tiny virtual Linux Apline only can run if Hypervisor is supported.
