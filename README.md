# coin-challenge

## What it does
Ansible playbook(s) that builds a Docker container for an Ethereum node, and runs it on EC2.

## How it works
This repository is continuously deployed via CircleCI, builds can be seen [here](https://circleci.com/gh/timmyers/workflows/coin-challenge/tree/master).

The CircleCI workflow is split into two jobs.

### build job
* ansible-container is used to build a container that runs go-ethereum.
  * Pulls version 1.8.3 of [go-ethereum source](https://github.com/ethereum/go-ethereum).
  * Builds executable from source.
* ansible-container is used to push resulting container to [dockerhub](https://hub.docker.com/r/timmyers/coin-challenge-go-ethereum/).

### deploy job
* ansible-playbook is used to deploy the container to an EC2 instance.
  * Initiates a docker container with a [Fedora Atomic AMI](https://getfedora.org/en/atomic/download/).
  * Pulls down the docker image previous pushed to dockerhub on the new EC2 instance.
  * Runs the docker container, starting the ethereum node on the EC2 instance.
