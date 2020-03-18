# kops
Kubernetes Operations

## install kubectl
`curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl`

`chmod +x ./kubectl`

`sudo mv ./kubectl /usr/local/bin/kubectl`

`kubectl version --client`

## kops create cluster yaml file

`kops create cluster --name=mycluster.tyagi.k8.net \
  --state=s3://tyagi.k8.net \
  --dns-zone=tyagi.k8.net --dns private --zones us-east-1a \
  --vpc=vpc-dae5a0a0 --subnets=subnet-e11f28cf \
  --networking=calico \
  --node-size=t3.large --node-count=2 --master-size=m4.large --master-count=1 \
  --dry-run \
  -oyaml > myk8cluster.yaml`

## kops create cluster
`kops create -f <filename.yml>`

`kops update cluster <cluster_name> --yes`

## kops update cluster
`kops replace -f <filename.yml>`

`kops update cluster <cluster_name> --yes` 

## kops rolling-upgrade cluster
Rolling upgrade one of the use case is vertically scale-in/out _"change in ec2 type"_
`kops replace -f <filename.yml>`

`kops rolling-update cluster <cluser_name> --yes`

`kops rolling-update cluster <cluster_name>  --yes --fail-on-validate-error="false" -node-interval 8m --instance-group nodes`
