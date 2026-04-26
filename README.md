#  Configuring Admission Controls in Kubernetes

## Overview
Implemented OPA Gatekeeper to enforce security policies using admission webhooks.

## What I Did
- Deployed OPA Gatekeeper v3.14
- Created ConstraintTemplate using Rego language
- Enforced non-root container policy
- Tested policy enforcement
- Configured exceptions using label selectors

## Key Commands
```bash
# Install Gatekeeper
kubectl apply -f https://raw.githubusercontent.com/open-policy-agent/gatekeeper/release-3.14/deploy/gatekeeper.yaml

# Apply constraint template
kubectl apply -f block-root-user-template.yaml

# Apply constraint
kubectl apply -f block-root-user-constraint.yaml

# Verify policy
kubectl get constrainttemplates
kubectl get k8srequiredsecuritycontext
```

## Results
| Test | Result |
|------|--------|
| Root container (UID 0) | ❌ Blocked |
| No securityContext | ❌ Blocked |
| Non-root container | ✅ Allowed |
| Exempt label pod | ✅ Allowed |

## Key Learning
Admission Controllers are the last line of defense 
before workloads are created in the cluster.

## Tools Used
- OPA Gatekeeper v3.14
- Rego Policy Language
- Kubernetes v1.35.1
- Minikube
