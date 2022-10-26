# SRE Checklist

Purpose: Provide teams and individuals an idea on what to aspire for or what to take into consideration in the SRE field and work

Clarification: these checklists are **opinionated**. They are based on my own opinion and experience and are not universal truth. So you should definitely doubt whatever you read here and more than welcome to add your own opinion on the matter

## Team

### SRE Team

#### Responsibilities

- [ ] Team responsibilities should be clear for everyone and documented
  - The common one are:
  - [ ] Managing infra
    - One can argue whether it's SRE or DevOps, but it depends on what functions the org has
  - [ ] Monitoring
  - [ ] App Performance (?)

#### Skills

- [ ] Coding!
  - It doesn't matter what language! market right now leaning towards mostly Go, but Python is also quite common and eventually whatever works better for the team
- [ ] Containers!
  - One can argue it depends on product and other considerations but I'm 100% confident you should understand containers to some extent
    - [ ] Kubernetes
      - If you agree about containers, Kubernetes is the next step (or other platforms like Nomad, but basically containers orchestration)
- [ ] Cloud (?)
    - Not sure if 100% tbh. I believe this very much depends on your infra in the org

#### Processes

- [ ] Incident Management
  - There must be a well defined process to how incidents are managed. Some thoughts:
    - Where incidents are reported/raised?
    - Who monitors the alerts at any given point of time?
    - Do you need 100% time coverage?
    - Is there any team that gets the alerts before the SRE team and tries to handle the issue?

### SRE Goals 

- [ ] Set goals
  - [ ] Define SLO (Service Level Objective)
  - 100% reliability is not a good goal (not sustainable + not feasible since you can drive 100% reliability for the service you own, but most of the time not for its dependencies)

### SRE Lead 

- [ ] Is there an onboarding page for SREs joining the team?
- [ ] Schedule 1:1 meeting with team (probably...manager or lead? TBD)
- [ ] Learn how others are doing it!
    - [ ] https://github.com/upgundecha/howtheysre - so many examples!
    - [ ] Personal favorite examples
      - [  ] [Enter the Abattoir](https://achievers.engineering/enter-the-abattoir-ee5e2019f0b3) - very cool idea of the SRE team to provide tooling around creation of "namespaces" - spaces with the all the components the dev team needs
- [ ] Identify Possible Gaps. Few things to watch our for:
  - [ ] Does development team waits on SRE for infra related operations?
  - [ ] Basically going over other check lists in this page :)
- [ ] Identify SRE team maturity and work on improving it
  - [ ] Step 1: Operations: SRE is focused on resolving issues, dealing with request
  - [ ] Step 2: Automation: SRE is moving towards automation and self-service. Providing tooling, documentation, etc.
  - [ ] Step 3: Product: SRE is focused on improving the product itself - reliability, performances, etc.

## Technologies

### Git Repositories

- [ ] Is there CI for every project?
  - [ ] Linting and Styling
  - [ ] Unit tests
  - [ ] E2E testing
- [ ] Infra is managed from code
  - [ ] IaC technology chosen and in use (Terraform, Ansible, Pulumi, etc.)

### Cloud

- [ ] Resources managed through IaC technologies such as Terrform, Pulumti, etc.
- [ ] Resources are tagged, labeled
  - [ ] Env (staging, prod, dev)
- [ ] Resources Quotas are set

### Kubernetes

- [ ] Apply/Add labels for every type of resources. You may use this [page](https://kubernetes.io/docs/concepts/overview/working-with-objects/common-labels) as a suggestion to which labels you should be adding
- [ ] CI/CD for Cluster bootstraping 
- [ ] CD process for manifests/configurations (using something like Flux, ArgoCD)
  - [ ] Make sure cluster bootstraping (the process of preparing the cluster) is managed fully using GitOps
- [ ] Cluster for each environment? Dev, QA, Staging, Production
  - [ ] Per region? Per cloud? How distributed your environment should be? 
- [ ] Cluster Policy Management
  - [ ] Networking Policies
  - [ ] Storage Policies

### GitOps - ArgoCD

- [ ] GitOps adopted for application deployments and rollouts
  - [ ] Infra code (Manifests, Configurations, etc.) is in a separate repository (and not in application repository)
- [ ] GitOps adopted for GitOps agents themselves and not only for app related code
  - [ ] DON'T install ArgoCD with kubectl commands
  - [ ] Helm chart not recommended as it lags behind official releases of new ArgoCD releases
  - [ ] Consider:
    - [ ] Hosted Argo CD instance (pros: maintenance is on others. cons: make sure you have some money in the wallet)
    - [ ] ArgoCD for managing ArgoCD (pros: easy DR, rollbacks, ... and full audit and changelog. cons: maintenance)
      - [ ] Consider using [Argo CD Pilot](https://argocd-autopilot.readthedocs.io/en/stable) for that which is "opinionated way of installing Argo-CD and managing GitOps repositories"
  - [ ] Think about:
    - [ ] One ArgoCD to control multiple clusters (why not: single point of failure)
    - [ ] Argo CD per cluster (why not: a lot of maintenance and basically over complexity)
- [ ] Sync Strategy
  - [ ] Auto Prune (resources deleted when files/content deleted)
  - [ ] Self-heal (cluster state corrected based on Git state and when manual changes done to the cluster)

## Monitoring

TODO

## Chaos Engineering

TODO
