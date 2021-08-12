# aws-asdi

## Getting Started
(*Optional*) Create a conda environment:
```sh
conda create -n aws-asdi python=3.7
```

Install dependencies:
```sh
pip3 install -r requirements.txt
```

(*Optional*) Installing data (if enough storage on drive):
```sh
mkdir data
aws s3 cp --recursive s3://noaa-ghcn-pds/csv/ --no-sign-request data
```

## Running on Single Node
```sh
jupyter notebook #or jupyter lab
```

## Scaling Through AWS Autoscalar
Make sure you have AWS credentials and keys stored and setup correctly, and we can start a cluster through:
```sh
ray up autoscaler-raw.yaml
```

Additionally, make sure the directory paths are configured correctly on lines 105 and 146.