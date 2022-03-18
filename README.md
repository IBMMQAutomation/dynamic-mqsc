# Dynamic MQSC

<img src="/readme-images/dynamic-mqsc-pipeline.png" width="55%" height="25%">

**Description**: This repo has a similar folder structure as our [gitops repo](https://github.com/IBMMQAutomation/mq-pipeline) for 5 different evironments such as DEV, SIT, UAT, PTE and PRD. Each environment has different queue manager folders and each queue manager folder has `dynamic.mqsc` and `.env`. In this pipeline, git-task will git clone this repo and inject values from all the `.env` files to its appropriate `dynamic.mqsc`. This way you can parameterized certains things such as route for receiver QM. Notice that `prd` and `pte` don't have dynamic mqsc files but have `.env` files because we will be promoting UAT mqsc to PTE then PRD

- Access: Developers will create PR and Admins will review and approve PRs

```
├── dev
│   ├── qm01
│   │   └── dynamic.mqsc
│   │   └── .env
│   └── qm02
│       └── dynamic.mqsc
│       └── .env
└── uat
    ├── qm01
    │   └── dynamic.mqsc
    │   └── .env
    └── qm02
        └── dynamic.mqsc
        └── .env

├── prd
│   ├── qm01
│       └── .env
│   └── qm02
│       └── .env
├── pte
│   ├── qm01
│       └── .env
│   └── qm02
│       └── .env

```

## Steps

### 1. Copy this repo to your enterprise repository

### 2. Make necessary changes to your MQSC files and pipeline.yaml

### 3. Apply tekton pipeline on openshift

Now, lets apply both of these files.

```
oc apply -f pipeline.yaml
oc apply -f git-task.yaml
```

### 4. Run the pipeline

Recommended: you can add webhook to trigger the pipeline run

Next Steps:

- Gitops (ArgoCD) - https://github.com/IBMMQAutomation/mq-pipeline
