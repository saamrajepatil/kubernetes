Setup for spring pet clinic on jenkins node

Need t2.medium ec2 

dowmload dokcer pipeline, kubernets cli, git,ECR plugins in jenkins.

Attach IAM role :  with admin access, EKS, ECR permisssons.



aws configure using jenkins user:

aws configure for jenkins user:
aws configure
access key :
secret key:
region us-east-1:




vi /etc/passwd
jenkins user

echo "jenkins ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/jenkins > /dev/null


login using jenins user :

curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.19.6/2021-01-05/bin/linux/amd64/kubectl
chmod +x ./kubectl
mv ./kubectl /usr/local/bin
kubectl version --short --client


curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin
eksctl version


Setup Kubernts cluser using jenkins user :

eksctl create cluster --name petclinicdev \
--region us-east-1 \
--node-type t2.micro \
--nodes-min 2 \
--nodes-max 2

check /var/lib/jenkins/.kube/config is present on the server.


Run the pipeline job using jenkinsfile from spring-petclinic repo

JAVA_HOME=/usr/lib/jvm/java-17-amazon-corretto
