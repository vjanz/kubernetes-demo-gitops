# kuberntes-demo-gitops
See the application source code: [kubernetes-demo-app](https://github.com/vjanz/kubernetes-demo-app)

## Project sturcture
```
├── apps
│   ├── argocd                              - Declarative ArgoCD applications
│   │   └── fastapi...yaml 
│   └── fastapi-service                     - One of the apps in GitOps
│       ├── base                            - Base of kustomization (common resources)
│       │   ├── deployment.yaml
│       │   ├── kustomization.yaml
│       │   └── service.yaml
│       └── overlays                       - Overlays of kustomization 
│           ├── development                - Environment specific resources
│           │   ├── ingress.yaml
│           │   ├── kustomization.yaml
│           │   ├── replica-count.yaml
│           │   └── sealed-secret.yaml
│           └── production
└── projects                                     - Separation of projects in ArgoCD
    └── fastapi-app.yaml

```

### Definition of GitOps Repository
A GitOps repository is supposed to hold files that are used to deploy applications. It is not supposed to hold application code. The application code is supposed to be in a separate repository. The GitOps repository is supposed to hold the following files:

- ArgoCD applications
- Kustomization files
- Environment specific resources
- Secrets
- ConfigMaps
- Helm charts
- Terraform files, etc.

Aside of adding new application to this repository, or updating existing application, the manifests should be modified by the CI/CD pipeline. The CI/CD pipeline should be responsible for building and pushing the application image, and updating the manifests with the new image tag on this repository