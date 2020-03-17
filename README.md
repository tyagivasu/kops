# kops
Kubernetes Operations

## kops create cluster yaml file

`----------------------------------------------------------------------------
  kops create cluster --name=mycluster.tyagi.k8.net \
  --state=s3://tyagi.k8.net \
  --dns-zone=tyagi.k8.net --dns private --zones us-east-1a \
  --vpc=vpc-dae5a0a0 --subnets=subnet-e11f28cf \
  --networking=calico \
  --node-size=t3.large --node-count=2 --master-size=m4.large --master-count=1 \
  --dry-run \
  -oyaml > myk8cluster.yaml
---------------------------------------------------------------------------`

# kops create cluster
`kops create -f <filename.yml>`
`kops update cluster <cluster_name> --yes`

# kops update cluster
`kops replace -f <filename.yml>`
`kops update cluster <cluster_name> --yes` 