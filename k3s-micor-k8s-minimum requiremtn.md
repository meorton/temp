| Distribution            | Resource Requirements Link | Notes                                                                                                                                                                      |
| ----------------------- | -------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **MicroK8s**            | Getting started minimums   | Lightweight, can run in ~540 MB RAM but recommended ≥4 GB + 20 GB disk for real workloads. ([Canonical][1])                                                                |
| **K3s**                 | K3s official prerequisites | Lightweight with minimal OS/hardware prerequisites; not strict CPU/RAM metrics on the main "requirements" page but known to run on small systems. ([K3s Documentation][2]) |
| **AKS Edge Essentials** | System requirements        | Official Microsoft requirements; includes supported Kubernetes versions and architectural guidance. ([Microsoft Learn][3])                                                 |

[1]: https://canonical.com/microk8s/docs/getting-started? "Get started"
[2]: https://docs.k3s.io/installation/requirements "Requirements"
[3]: https://learn.microsoft.com/en-us/azure/aks/aksarc/aks-edge-system-requirements "AKS Edge Essentials system requirements - Azure"




From Azure Arc–enabled Kubernetes system requirements:

Azure Arc agents require:

~850 MB of free memory

~7% of a single CPU core

📎 Source (official):
https://learn.microsoft.com/azure/azure-arc/kubernetes/system-requirements



Minimum platform requirements (cluster only, no workloads)
Platform	Local only (K8s platform)	With Azure Arc + GitOps (Flux)
AKS Edge Essentials	4 GB RAM / 2 vCPU	4 GB + 850 MB RAM / 2 vCPU + ~7% CPU
K3s (Ubuntu/Linux)	1 GB RAM / 1 vCPU	1 GB + 850 MB RAM / 1 vCPU + ~7% CPU
MicroK8s (Ubuntu/Linux)	~540 MB RAM / 1 vCPU	~540 MB + 850 MB RAM / 1 vCPU + ~7% CPU
