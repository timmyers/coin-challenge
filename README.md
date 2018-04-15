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

## TODO's (future improvements)
* Start geth as a full node (currently running `--syncmode "light"` to be faster).
* Deploy with a persistent storage volume, so that node doesn't have to resync from scratch on every deploy (duh)
* DNS - Create a consistent DNS endpoint where the node's RPC API can be accessed.
* Implement security of RPC endpoint so that not just anyone can access it.
* Use alpine linux for container so that resulting image is not so big.
* Leverage a Kubernetes cluster to orchestrate container deployments, rather than a single EC2 instance.
* Automatically update and deploy when geth repository has a new version.
* Implement some testing into the deploy process to verify that the new node is operating as expected.
* Lock down the master branch, and create a PR workflow that builds (and ideally tests) new versions of code before they may be merged in.
