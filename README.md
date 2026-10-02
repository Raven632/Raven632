# Khalil Velinov

Junior DevOps engineer in TODO-CITY, Germany. I build infrastructure on Proxmox, automate it with
Terraform and Ansible, and run my own apps in Docker with CI/CD.

- **Looking for:** TODO-ROLE (for example: a junior DevOps or Linux admin position, full-time or as a
  working student), from TODO-DATE
- **Languages:** German (TODO), English (TODO), Russian (TODO)
- **Contact:** [TODO-EMAIL](mailto:TODO-EMAIL) · [LinkedIn](TODO-LINK) · [CV (PDF)](TODO-LINK)

### Experience

**DevOps intern, partimus GmbH** (Limburg, May to June 2026)

- set up a 3-node Proxmox VE cluster with Ceph and SDN
- moved VM provisioning to Terraform (Cloud-Init templates, state in MinIO) and Ansible;
  every change goes through a Forgejo CI pipeline, nobody runs `terraform apply` by hand
- deployed authentik as the single login (OIDC) for the lab, Fedora CoreOS with Butane/Ignition
- built Kubernetes by hand (Kubernetes The Hard Way) and worked through the K8sQuest challenges

<details>
<summary>How the lab is wired</summary>

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

</details>

Code and notes: [Praktika_](https://github.com/Raven632/Praktika_)

### Projects

**[RPG Library](https://github.com/Raven632/rpg-library)**: a self-hosted web app for playing RPG Maker
games in the browser, which I build and run on my home server. Node.js, React, SQLite, Redis, Docker.
In development since March 2026 (200+ commits). GitHub Actions runs the tests, and the server deploys
new versions itself, checks that they start and rolls back if they don't. Games run on a separate
origin, so their scripts can't touch the library API.

<details>
<summary>Screenshot</summary>

<img src="https://raw.githubusercontent.com/Raven632/rpg-library/main/rest/img/library.png" alt="RPG Library" width="700">

</details>

**[City of Code](https://github.com/Raven632/City-of-Code)**: a school team project (three of us,
until March 2027), a browser game that teaches Python. I'm the project lead and do the backend,
which I'm learning as I build it: Flask, JWT, SQLAlchemy, Docker on a VPS. Student code runs in the
browser with Pyodide, never on our server. The database design is done, the API is next.

**Homelab**: Proxmox with Docker. My apps run there as prod and dev stacks, deploys and backups are
systemd timers, alerts go to Telegram, access over Tailscale.

### Skills

Proxmox, Ceph, Linux, Bash, Terraform, Ansible, Cloud-Init, Docker, Kubernetes, Forgejo CI,
GitHub Actions, authentik, MinIO, Node.js, React, Python, Flask, SQLAlchemy, SQLite, Redis

### Education

- IT at Friedrich-Dessauer-Schule, Limburg (TODO: name of the program, until TODO)
- B.Sc. Software Engineering, TODO-UNIVERSITY (expected TODO)
- preparing for HashiCorp Certified: Terraform Associate
