# how-to-use-dirk
This is an example about how to use dirk. dirk stands for direnv kubeconfig and makes it easy to connect to multiple kubernetes clusters depending on the current working directory. In this tutorial we will use py-dirk - the Python implementation of dirk.

# Requirements
The following requirements are considered to be given:
- *nix
- direnv
- Python3
- minikube
- kubectl

# Use dirk

## Get the code
Get the code - e.g. like this:

```bash
git clone https://github.com/deepshore/how-to-use-dirk
```

## Create and activate a virtual environment
Enter the project folder and create a venv like this:

```bash
cd how-to-use-dirk
python3 -m venv venv
```

Activate it:

```bash
source venv/bin/activate
```

## Install py-dirk
Install py-dirk using pip:

```bash
pip install py-dirk
```

## Init dirk in dev and prod
Init dirk in the dev and prod folder like this:

```bash
dirk init dev 
dirk init prod
```

## Bind minikube clusters to project folders
Change directory to dev and create a minikube cluster with profile name dev:

```bash
cd dev && minikube start -p dev
```

minikube will add the configurations for connecting to the dev cluster to the dev/kubeconfig file.

Repeat the step above for prod:

```bash
cd ../prod && minikube start -p prod
```

## Check if it is working

There should currently be at least two minikube clusters running - dev and prod:

```bash
minikube profile list
```

Make sure that you are talking to the prod cluster by considering the name of the node:

```bash
kubectl get nodes
```

If you change to the dev directory, kubectl is now connected to the dev cluster:

```bash
cd ../dev && kubectl get nodes
```

## Init directory using an existing kubeconfig

You can bind the existing dev/kubeconfig to the another-dev folder like this:

```bash
dirk init another-dev -c dev/kubeconfig
```

# Clean up

Stop all of the minikube clusters like this:

```bash
minikube stop --all
```

Delete the dev and the prod cluster like this:

```bash
minikube delete -p dev
minikube delete -p prod
```

# Additional remarks

Note that .envrc and kubeconfig should generally not be added to a repository.
