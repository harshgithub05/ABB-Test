# ABB-Test

# 1. Task: Infrastructure as Code (IaC) Design (Terraform or Bicep):
<!-- To run terraform module. -->
<!-- First we will run terraform init command to initialize the moudle. -->

    terraform init -reconfigure -input=false -backend-config="client_id=xxxxxxx" -backend-config="client_secret=xxxxxxx" -backend-config="subscription_id=xxxxxxx" -backend-config="tenant_id=xxxxxxx"

<!-- after init we will run plan and verify all the resource configuration -->

    terraform plan -var-file="environment/dev.tfvars" -out terraform.tfplan

<!-- once all things looks good in plan lets deploy the resources. -->

    terraform apply --auto-approve "terraform.tfplan"

# 2. Task: CI/CD Pipeline Setup using GitHub Actions
    <!-- Setup the CI/CD workflow in Github Action. 
    Created the pipeline to checkout the repository and the pipeline also included commented code which can be used for build purpose.
    Apart from that pipeline contains the code for deploying helm chart using github action workflow. -->

    Steps for setting up the workflow to deploy Helm chart
    1. We need to enable read-write workflows access
    click the Settings -> Actions > General -> workflow permission -> select Read and write permissions.

    2. Registry Token for connecting to Docker hub to pull the image.
        Go in Secutiry -> secret variable.
        Later use this variable name inside you workflow pipeline.

    3. Setup KUBECONFIG
        Add another secret for your Kubeconfig file, name the secret as KUBECONFIG and paste in your Kubeconfig contents. Your workflow will use these credentials to connect to your Kubernetes cluster and complete your deployment. -->



# 3. Task:Shift Left Security (Secret Scanning and Code Security):

    <!-- To acheive this we need to enable Code security and secret protection in Github repo:
    To do so we first need to make sure that our repo is PUBLIC otherwise scanning options are greyed and we won't be able to enable it.
    To enable it. click on Security -> code security -> Code Scanning -> Enable CodeQL analysis.

    CodeQL is default scanning and analysis tool offered by Github, it uses opensource recommendation and perform scanning 
    based on it. 
    Once CodeQL is enable it will make sure to run before our CI/CD pipeline and also help us to give the result.
    There is another option Secret Protection which I enabled to make sure that token, secrets, keys are not exposed. -->

# 4. Task: Helm-Based Deployment in AKS:
    <!-- The helm chart is being present under helm folder
    Helm chart is being created for running AI application.
    used AI image from docker hub "ai/chat-demo-model" which is running on port 11434. Currently used latest tag for the exercise.  -->

# 5. Task: GitOps with ArgoCD
    <!-- We need to down agro cli in our runner either shared or self-hosted. Better to use self-hosted with our own specification.
    argocd app create ai-app \
	--repo https://github.com/harshgithub05/ABB-Test.git \
	--path ABB-Test/helm/ \
	--dest-server https://kubernetes.default.svc \
	--dest-namespace ai-app \
	--sync-option CreateNamespace=true \
	--parameter namespace=ai-app \
    application 'ai-app' created -->

