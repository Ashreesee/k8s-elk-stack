# Step for the Tutorial

### pre-required things:
</br>


Create a IAM User -> With Policies as below:
</br>
	AdministratorAccess, AmazonEKSClusterPolicy
 
 </br>
  Then Click on User(new) which you just created now -> and click on Security Credentials -> Click on " Create access key "
 </br> 
  -> after Clicking on Create Access Key - It will ask for UseCase
  </br>
  -> USE CASE: CLI
  </br>
  -> Ignore the next step
  </br>
  -> Generate the Keys
  </br>
	-> Copy the access key and Secret key before click on finish Button ( as it will not show again after this)
 </br>


  
  Launching the Ec2 - ubuntu instance  </br>
  
  
   ####  installation of AWS CLI  #######
   </br>
  https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html
   </br>
  sudo apt update
 </br>
	curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
 </br>
	sudo apt install unzip
   </br>
	unzip awscliv2.zip

 </br>
	sudo ./aws/install
	 </br>
	aws --version
  
   </br>
## Install eksctl 
 </br>
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
 </br>
sudo mv /tmp/eksctl /usr/local/bin
 </br>
eksctl version
 </br>
#######################################################################################################################################################################
   </br>
  >> aws configure with access key and secret key along with region (us-east-1 / mumbai / ap-south-1)
 </br>
	>> aws configure </br>
  >> access key </br>
  >> secret key </br>
  >> region </br>
  >> json </br>
  
  ########################################################################################################################################################################
 </br>
 
###################################    installing k8s client (kubectl):     ################################################################################################

installing k8s client (kubectl): </br>

curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.30.2/2024-07-12/bin/linux/amd64/kubectl </br>
>> curl get from web - the package of eks - from aws release </br>

  curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.30.2/2024-07-12/bin/linux/amd64/kubectl.sha256 </br>
>> curl get from web - the package of eks - from aws release(with production Stack) </br>
 </br>
sha256sum -c kubectl.sha256 </br>
>> do a check - weather it is sha256 verified package or not </br>

openssl sha1 -sha256 kubectl </br>

chmod +x ./kubectl </br>
>> add the execute permission for kubectl package </br>

mkdir -p $HOME/bin && cp ./kubectl $HOME/bin/kubectl && export PATH=$HOME/bin:$PATH </br>
>> assigning the package of kubectl in the bin / directory as ubuntu can identify the k8s package </br>

kubectl version --client </br>
>> verifying the installation </br>





###################################    Cluster Creation EKS with ManagedNode Group in aws eks :     ################################################################################################
  
eksctl create cluster --name my-testcluster --region us-east-1 --nodes 3 --node-type t3.medium </br>
>> taking 5-10mins to perform the thing </br>
>> while above command is executing -  we can take a look in the cloudfomration portal - so that the things are in progress / or not! </br>
 </br>
>> cost optimized commands for cluster creation </br>
>>>>>> eksctl create cluster --name my-cluster --region us-east-1 --nodes 2 --node-type t2.micro </br>
 </br>

