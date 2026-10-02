# Khalil Velinov

Junior DevOps engineer. Studying IT while finishing my B.Sc. in Software Engineering.
Most of what I build runs on Proxmox at home, and I try to automate whatever I end up doing twice.

Right now I'm preparing for the HashiCorp Terraform Associate exam.

### Internship at partimus GmbH (Limburg, May to June 2026)

Two months of DevOps work on a Proxmox lab where nothing gets clicked together in the web UI:
every VM and service comes from a commit.

```
                     ┌──────────────────────────┐
   git commit  ────► │  Forgejo (self-hosted)   │
                     │  CI/CD pipeline          │
                     └────────────┬─────────────┘
                                  │
                    ┌─────────────┴──────────────┐
                    ▼                            ▼
            ┌───────────────┐            ┌───────────────┐
            │   Terraform   │            │    Ansible    │
            │  (provision)  │            │  (configure)  │
            └───────┬───────┘            └───────┬───────┘
                    │                            │
                    │  state ──► MinIO (S3)      │
                    │                            │
                    ▼                            ▼
      ┌──────────────────────────────────────────────────┐
      │        Proxmox VE, 3-node HA cluster             │
      │        Ceph storage  ·  SDN  ·  PegaProx         │
      ├──────────────────────────────────────────────────┤
      │  VMs / CTs  ·  Fedora CoreOS  ·  Kubernetes      │
      │  authentik (SSO / OIDC)                          │
      └──────────────────────────────────────────────────┘
```

- set up the 3-node cluster with Ceph and SDN (three nodes is the minimum for a Ceph quorum and
  real HA)
- Terraform clones VMs from a Cloud-Init template. State is in MinIO, so `terraform apply` only runs
  in CI, never from someone's laptop, and credentials come from CI secrets
- built the same VM setup a second time with Ansible only, to compare the two tools on one task
- authentik as the single login (OIDC) for the cluster. Its secrets are generated on the host during
  the deploy, nothing is committed
- Fedora CoreOS VMs configured with Butane, turned into Ignition by Terraform at apply time
- set up Kubernetes by hand following Kubernetes The Hard Way (etcd, API server, kubelet, TLS, CNI),
  then worked through the K8sQuest troubleshooting challenges

Code and notes: [Praktika_](https://github.com/Raven632/Praktika_)

### City of Code (school project, in progress)

A team project at the Friedrich-Dessauer-Schule in Limburg, August 2026 to March 2027: a browser game
that teaches Python. Students write code in an editor in the browser, and every task they solve adds a
building to their own 2D city. There are three of us. I'm the project lead and I do the backend,
the database and the deployment. Backend work is new to me, so I'm learning it while I write it.

- student code never runs on our server: it runs in the browser with Pyodide inside a Web Worker,
  and the worker gets killed if a solution loops forever
- Flask API with JWT: students sign up with a class code, teachers get an overview of their class
- SQLAlchemy on SQLite, deployed with Docker on a VPS (Gunicorn behind Nginx)
- we planned it properly: a requirements spec with a test for every requirement and a network plan
  with a critical path to the deadline

So far the database design is done (7 tables, documented with an ER diagram), the Flask API is next.

Code: [City-of-Code](https://github.com/Raven632/City-of-Code)

### RPG Library

I wanted to play my RPG Maker games from my home server on my phone, so I wrote
[rpg-library](https://github.com/Raven632/rpg-library). I've been working on it since March 2026
(200+ commits) and it runs on my server for real use.

- Node.js/Express backend with SQLite and Redis, React frontend
- games run on their own origin (separate port, per-game keys, CSP), so a game's scripts can't call
  the library API
- uploads go in chunks and continue after a dropped connection. One bug took me a while: on iOS the
  response to a big upload request never arrives, so the client now checks every chunk with a
  separate small request
- cloud saves with history, and an old save from a phone that was offline can't overwrite a newer one
- GitHub Actions runs the tests, the server pulls new versions on its own, checks that they start and
  rolls back if they don't

<img src="https://raw.githubusercontent.com/Raven632/rpg-library/main/rest/img/library.png" alt="RPG Library" width="700">

### Homelab

Proxmox with Docker on top. The library runs there as a prod and a dev stack, deploys and backups are
systemd timers, alerts go to Telegram, and I reach everything over Tailscale.

### Tools

Proxmox, Ceph, Linux, Terraform, Ansible, Cloud-Init, Fedora CoreOS, Kubernetes, Docker, Forgejo CI,
GitHub Actions, authentik, MinIO, Bash, Node.js, React, Python, Flask, SQLAlchemy, SQLite, Redis,
Playwright
