# kops
Kubernetes Operations

## install kubectl
```
1. curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl`
2. chmod +x ./kubectl
3. sudo mv ./kubectl /usr/local/bin/kubectl`
4. kubectl version --client
```

## install kops
```
curl -LO https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64
chmod +x kops-linux-amd64
sudo mv kops-linux-amd64 /usr/local/bin/kops
```

## kops create cluster yaml file

```
kops create cluster --name=mycluster.tyagi.k8.net \
--state=s3://tyagi.k8.net \
--dns-zone=tyagi.k8.net --dns private --zones us-east-1a \
--vpc=vpc-dae5a0a0 --subnets=subnet-e11f28cf \
--networking=calico \
--node-size=t3.large --node-count=2 --master-size=m4.large --master-count=1 \
--dry-run \
-oyaml > myk8cluster.yaml
```

```
Exporting KOPS_STATE_STORE is must before running any of below commands.

export KOPS_STATE_STORE="s3://INSERT S3 BUCKET HERE"
```
## kops create cluster
```
export KOPS_STATE_STORE="s3://INSERT S3 BUCKET HERE"

1. kops create -f <filename.yml>
2. kops update cluster <cluster_name> --yes`
```

## kops update cluster
```
export KOPS_STATE_STORE="s3://INSERT S3 BUCKET HERE"

1. kops replace -f <filename.yml>
2. kops update cluster <cluster_name> --yes
```

## kops rolling-upgrade cluster
Rolling upgrade one of the use case is vertically scale-in/out _"change in ec2 type"_
```
1. kops replace -f <filename.yml>
2. kops rolling-update cluster <cluser_name> --yes
or
kops rolling-update cluster <cluster_name>  --yes --fail-on-validate-error="false" -node-interval 8m --instance-group nodes
```
