# Product Requirements Document (PRD): Kubernetes EC2 Operator

**Product Name**: EC2 Operator  
**Version**: 0.1.0 (MVP following freeCodeCamp course)  
**Owner**: Cesar (Junior Pupil) + Grok (Distinguished Engineer Mentor)  
**Goal**: Extend Kubernetes to declaratively manage AWS EC2 instances via Custom Resources.  
**Target Users**: Platform engineers, devs wanting GitOps for EC2 provisioning.  
**Non-Goals (for MVP)**: Multi-region, auto-scaling, EBS volumes, advanced networking, production HA operator deployment.

## Epic 1: Core Operator Scaffolding & CRD
- [ ] Initialize Kubebuilder project with correct domain/repo
- [ ] Define EC2Instance CRD (v1) with meaningful .spec and .status
- [ ] Generate manifests & deepcopies

## Epic 2: Reconcile Loop Basics (Happy Path)
- [ ] Implement Observe → Compare → Act loop
- [ ] Integrate AWS SDK Go to create EC2 instance
- [ ] Update .status with instance ID, state, public IP

## Epic 3: Idempotency & Error Handling
- [ ] Ensure reconcile is idempotent (no duplicate instances)
- [ ] Handle sad paths (AWS errors, rate limits) with requeue
- [ ] Add logging + Kubernetes events

## Epic 4: Finalizers & Cleanup
- [ ] Add finalizer to CR
- [ ] Implement deletion: terminate EC2 on CR delete
- [ ] Wait for termination confirmation

## Epic 5: Testing & Validation
- [ ] Unit tests for controller logic
- [ ] Integration/e2e: local K3D + sample CR apply → verify in AWS console
- [ ] Basic validation/defaulting webhooks (optional stretch)

## Epic 6: Packaging & Deployment
- [ ] Build Docker image
- [ ] Generate Helm chart
- [ ] Deploy operator + sample CR to local cluster
- [ ] RBAC: minimal permissions only
- [ ] Secrets handling for AWS creds

## Success Criteria (MVP Done)
- Apply `EC2Instance` CR → EC2 launches in AWS
- Delete CR → EC2 terminates cleanly
- Operator runs locally without crashes
- No hard-coded secrets
- Follows Kubebuilder best practices (idempotency, finalizers, events)

References:
- Course: https://www.youtube.com/watch?v=odP153inZUo
- Reference Repo: https://github.com/shkatara/kubernetes-ec2-operator
- Kubebuilder Book: https://book.kubebuilder.io (esp. good-practices, finalizers)
