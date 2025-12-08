Reflections
GitOps Implementation with ArgoCD
Overview

During the final phase of the project, I implemented a GitOps workflow using ArgoCD to automate Kubernetes deployments. This approach replaced manual Helm installations with a continuous delivery process driven entirely by version control. The manifests and Helm chart references were stored in a dedicated GitOps repository, and ArgoCD automatically synchronized them with the Kubernetes cluster.

ArgoCD continuously monitored the repository for changes and deployed updates whenever new commits were pushed, ensuring that the cluster state always matched the declared configuration in Git.

Benefits of Using ArgoCD (GitOps) Over Manual Helm Deployments
1. Automation and Continuous Delivery

ArgoCD automates the deployment pipeline — once code is merged, changes are applied to the cluster automatically.

Eliminates the need for manual helm install or helm upgrade commands.

Supports automatic sync, rollback, and self-healing features.

2. Single Source of Truth

The Git repository becomes the authoritative source for cluster configuration.

Every change is tracked, versioned, and auditable.

Makes it easy to reproduce environments or roll back to a stable version.

3. Improved Collaboration and Transparency

All changes are visible in Git history and through the ArgoCD web UI.

Team members can review, approve, and audit infrastructure updates.

Reduces configuration drift and human error.

4. Visual Management and Monitoring

ArgoCD provides a real-time UI showing the health and sync status of every application.

Makes debugging and rollback straightforward.

Challenges and Lessons Learned
1. Initial Setup Complexity

Installing ArgoCD and configuring RBAC, namespaces, and repository access required more setup time than manual Helm commands.

Managing secrets (e.g., private Git repo access) added another layer of complexity.

2. Debugging Sync and Permission Issues

Early sync failures were often caused by misconfigured paths or service accounts.

Understanding ArgoCD’s Application manifest structure and syncPolicy options was essential for stability.

3. Dependency Management

Managing service dependencies (e.g., PostgreSQL before Catalog) required defining clear deployment order or using the App of Apps pattern.

Helm’s dependency mechanism was simpler in small environments, but ArgoCD offered more control for multi-service systems.

4. State Synchronization

At times, ArgoCD’s live state didn’t immediately reflect manual kubectl changes.

Learned to always commit changes to Git rather than applying them manually to maintain full GitOps integrity.

Comparison Summary
Aspect	Manual Helm Deployment	ArgoCD (GitOps)
Deployment Control	Manual commands (helm install, helm upgrade)	Automated sync from Git
Visibility	CLI only	Real-time web dashboard
Version Tracking	Limited (requires manual tracking)	Built-in Git history and rollback
Team Collaboration	Requires coordination	Git-based review and audit
Setup Complexity	Simple	Higher initial setup
Scalability	Works well for small apps	Ideal for multi-service, multi-environment systems
Final Reflection

Using ArgoCD completely changed how I approached Kubernetes deployments. While Helm is great for manual, one-off deployments, ArgoCD’s GitOps model enforces discipline, visibility, and automation.
It ensures that the running environment always matches what’s defined in Git — a key DevOps principle.

This experience reinforced the value of declarative infrastructure, automation, and version control as a single source of truth. Though ArgoCD required more setup time, the long-term benefits of reliability and scalability made it the superior choice for production-grade workflows.
