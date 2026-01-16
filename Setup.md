# Setup Guide: Local Development Environment

**Prerequisites** (verify before anything):
- [ ] Go ≥ 1.23: `go version`
- [ ] Docker Desktop running
- [ ] kubectl: `kubectl version --client`
- [ ] K3D: `k3d --version` (install: curl -s https://raw.githubusercontent.com/k3d-io/k3d/main/install.sh | bash)
- [ ] Kubebuilder ≥ v4.x: `kubebuilder version` (install: curl -L -o kubebuilder https://go.kubebuilder.io/dl/latest/$(go env GOOS)/$(go env GOARCH) && chmod +x kubebuilder && mv kubebuilder ~/bin/)
- [ ] AWS CLI (optional but helpful): `aws --version`
- [ ] Git Bash / VS Code terminal configured

**AWS IAM Setup** (critical – do not skip):
- [ ] Regain root access or create dedicated IAM user "ec2-operator-dev"
- [ ] Attach policy: AmazonEC2FullAccess (MVP; narrow later)
- [ ] Generate access key pair → NEVER commit
- [ ] Store safely: Use ~/.aws/credentials [default] or export env vars in terminal

**One-Time Cluster Setup**:
- [ ] Create local cluster: `k3d cluster create ec2op --port '8080:80@loadbalancer'`
- [ ] Set context: `kubectl config use-context k3d-ec2op`

**Daily Dev Workflow**:
1. Open VS Code → terminal (Git Bash)
2. Export AWS creds (Option A – quick):
   ```bash
   export AWS_ACCESS_KEY_ID=AKIA...
   export AWS_SECRET_ACCESS_KEY=...
   export AWS_REGION=us-west-2   # your choice
