### 1) GitHub Actions (CI) to build a jar and (optionally) a Docker image for every push to master.  
Add the file .github/workflows/ci-deploy.yml  

### 2) install terraform and aws cli (optional for windows)
```bash
winget install -e --id Amazon.AWSCLI
winget install -e --id Hashicorp.Terraform

# set up aws credentials
aws configure
# generate an ssh key pair for ec2 instance access
ssh-keygen -t ed25519 -f ~/.ssh/terraform-ec2 -C "terraform-ec2"

cd infra
terraform init
terraform apply
```

### 3) Add AWS and Terraform secrets to GitHub Actions
git repository -> Settings -> Secrets and variables → Actions → New repository secret  
```bash
EC2_HOST = ec2 ip  
EC2_SSH_KEY = cat ~/.ssh/terraform-ec2
```

The Docker image in GHCR (GitHub Container Registry) and deploy via SSH  
.github/workflows/ci-deploy.yml # everything was combined in 1 file for the simplicity purpose  

* If a Github Action fails for docker pull -> make GHCR repository public in the Github profile

### 4) Access the application
```bash
curl <EC2_IP>/actuator/health
curl <EC2_IP>/hello
```