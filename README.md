# Khalil Velinov

Junior DevOps engineer. Studying IT while finishing my B.Sc. in Software Engineering.
Most of what I build runs on Proxmox at home, and I try to automate whatever I end up doing twice.

Right now I'm preparing for the HashiCorp Terraform Associate exam.

### Internship at partimus GmbH (Limburg, May to June 2026)

During my DevOps internship I set up a 3-node Proxmox VE cluster with Ceph and SDN and moved VM
provisioning to Terraform and Ansible. Terraform state is stored in MinIO, changes go through a Forgejo
pipeline instead of someone running `terraform apply` on their laptop, and logins go through authentik
(OIDC). I also built Kubernetes by hand following Kubernetes The Hard Way, mostly to see what the
installers normally hide from you.

Code and notes: [Praktika_](https://github.com/Raven632/Praktika_)

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

Proxmox, Ceph, Linux, Terraform, Ansible, Cloud-Init, Kubernetes, Docker, Forgejo CI, GitHub Actions,
authentik, MinIO, Bash, Node.js, React, SQLite, Redis, Playwright
