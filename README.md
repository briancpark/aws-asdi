# AWS-ASDI Project
Scaling up Data Science Workflow/Pipeline with Ray Environment Through NOAA-GHCN Dataset

## Getting Started
(*Optional*) Create a conda environment:
```sh
conda create -n aws-asdi python=3.7
conda activate aws-asdi
```

Install dependencies:
```sh
pip3 install -r requirements.txt
```

## Running on Single Node
This project was developed on a single node with 32 cores/64 threads and 512GB of memory. A r5.16xlarge EC2 instance will be sufficient enough to run.

(*Optional, but recommended*) Installing data (~100GB in size):
```sh
mkdir data
aws s3 cp --recursive s3://noaa-ghcn-pds/csv/ --no-sign-request data
```

Run/execute notebook:
```sh
jupyter notebook #or jupyter lab
```

## Scaling with Multiple Nodes Through AWS Autoscaler
Make sure you have AWS credentials and keys stored and setup correctly, and we can start a cluster from our local machine conveniently through:
```sh
ray up autoscaler-raw.yaml
```

*Additionally, make sure the directory paths to your local machine are configured correctly on lines 105*

The autoscaler script is configured with 1 head node, 4 worker nodes on us-east-1. It is important to make sure the worker nodes have initialized and started properly, otherwise the cluster configuration may fail to recognize worker nodes. To make sure a Ray cluster has started properly, check it by running this command from our local machine and view [localhost:8265](localhost:8265)(There should be 5 nodes):
```sh
ray dashboard autoscaler-raw.yaml
```
or check it through:
```sh
ray attach autoscaler-raw.yaml
ray status #once connected to remote EC2 instance
```

To run and execute the notebook, port forward the Jupyter notebook to connect it to your local machine's browser:
```sh
ssh -i <path/to/pem/file> -N -f -L localhost:8888:localhost:8888 ec2-user@<public.ipv4.address>
```

Once done, you can properly shutdown the cluster by running:
```sh
ray down autoscaler-raw.yaml
```