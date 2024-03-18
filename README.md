This repo contains a Terraform configuration file to provision an EKS cluster on AWS.

Steps:

1. Configure AWS CLI by following: https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html



2. Launch your AWS command line and run the following command:

aws configure

Then provide your AWS account credentials:

AWS Access Key ID
AWS Secret Access Key
Default region name



3. In the main.tf file you will see the terraform template to deploy an EKS Cluster on AWS. To be able to run this terrafom template,
first install terraform on your environment by following the reference: https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli

Verify terraform was installed correctly by running: terraform version



4. Run the "terraform init" command to initialize the  working directory containing the configuration files which installs plugins for required providers.
After this, run the "terraform plan" command. With this you’ll be able to preview the above Terraform configuration file (main.tf) and the resource that will be created:

terraform plan

Then run the "terraform apply" command. The terraform apply command executes the actions proposed in a Terraform plan:

terraform apply --auto-approve



5. In the AWS Web Console, please go to EKS and you will see your AWS Cluster. To access your AWS EKS clustter, please type the following on your terminal:

aws eks --region example_region update-kubeconfig --name cluster_name

Note: Replace example_region with the name of your AWS Region. Replace cluster_name with your EKS cluster name. 



6. The "terraform destroy" command will allow you to destroy all remote objects managed by a particular Terraform configuration.



7. To deploy a container on this EKS cluster:

7.1: Create your Docker image

Please save your dockerfile in your working directory. Then follow the "docker build -t <image_name> . " command to generate your docker image. To see your docker image 
just run the following command: "docker images"

7.2: After building, run the following docker tag command to tag the image:

docker tag <image_name>:<version>

7.3: Create your kubernetes depoyment by using your recently created docker image. For this use the "kubectl create -f deployment.yaml" command. Then
run: "kubectl get deployment <deployment_name> to see the status of your deployment. Also run: "kubectl get pods" and you will see the kubernetes pod running your docker image.

7.4: Create the kubernetes service that will expose your application: "kubectl create -f svc.yaml". Run "kubectl get svc" to review the service parameters.


 

