### 1) GitHub Actions (CI) to build a jar and (optionally) a Docker image for every push to master.  
Add the file .github/workflows/ci.yml  

### 3) install terraform and aws cli (optional for windows)
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

git repository -> Settings -> Secrets and variables → Actions → New repository secret  
```bash
EC2_HOST = ec2 ip  
EC2_SSH_KEY = cat ~/.ssh/terraform-ec2
```

Make Docker image in GHCR and deploy via SSH
.github/workflows/deploy.yml
