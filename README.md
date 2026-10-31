# Homelab Project

I've created this repo to track my self-hosted / homelab journey.

## Goals

- Improve my Docker and container skills  
- Build a self-hosted media server  
- Centralise storage across devices  
- Improve Linux, networking, and DevOps skills  
- Build a hands-on homelab focused on networking, self-hosting, and system experimentation 

## Cybersecurity Goals

- Implement a secure home network architecture (segmented services where possible)  
- Use DNS filtering (AdGuard Home / Pi-hole / Technitium DNS) to reduce malicious traffic  
- Enforce secure remote access using VPN (WireGuard / Tailscale) instead of port forwarding  
- Harden all self-hosted services (disable default credentials, use strong authentication)  
- Implement regular vulnerability updates for Docker containers and host systems  
- Apply least-privilege access principles across services and NAS shares  
- Introduce monitoring and alerting for unusual activity (Uptime Kuma / Grafana later expansion)  
- Secure backups with encryption (aligned with 3-2-1 principles)  

## Hardware

### 🖥 Gaming PC (Primary Workstation)

- **Operating System:** Windows 11 Pro  
- **CPU:** AMD Ryzen 5 3600 (6 cores / 12 threads, 3.6GHz base / 4.2GHz boost)  
- **Motherboard:** MSI B450 Gaming Pro Carbon AC (MS-7B85, AM4)  
- **Memory:** 32GB DDR4 G.Skill Trident Z Neo RGB (2×16GB, 3600MHz CL16, XMP 2.0)  

- **Storage:**
  - 1TB Crucial P1 NVMe SSD (PCIe Gen3, up to 2000MB/s read)
  - 2TB Crucial BX500 SATA SSD
  - 2TB Seagate BarraCuda 2.5" HDD (5400RPM)

- **Power Supply:** SilverStone 750W 80+ Gold (semi-modular)  
- **Case:** Cooler Master MasterBox MB530P (ATX, tempered glass, ARGB airflow)

### 🗄 NAS (Network Attached Storage)

- **Model:** TerraMaster F4-425  
- **Storage:**
  - 1× Toshiba N300 4TB 3.5" NAS HDD (SATA 6.0 Gbit/s, 512MB cache, 7200 RPM)

- **Network:** Connected via Tenda Nova MW6 Mesh Ethernet backhaul (via node)

### 🍓 Raspberry Pi (Edge / Utility Device)

- **Model:** Raspberry Pi 4 Model B (1GB RAM)  
- **Storage:** 16GB MicroSD Card (Class 10)

## Services (Implementation Priority)

### 🔴 Phase 1 — Infrastructure Platform (Base System)

- **Virtualisation Platform** — Proxmox — Host for VMs and containers (core infrastructure layer), running as a two-node cluster on the mini PCs  
- **Cluster Quorum** — Corosync QDevice on the Raspberry Pi — Third quorum vote, so one node can be down without the cluster locking its config  
- **IP Reservations** — TP-Link Archer AX55 Pro — DHCP reservations for the NAS, both Proxmox nodes and the Raspberry Pi  
- **Lab Switching** — VLAN-capable managed switch (or a direct link between nodes) — Lets lab VMs on either node reach the OPNsense LAN  
- **Lab Router & Firewall** — OPNsense (VM) — Routes and segments the lab; WAN and LAN bridges exist on both nodes so it can migrate  
- **DNS & Network Control** — Pi-hole / AdGuard Home / Technitium DNS — Network-wide DNS filtering and control  
- **Remote Access VPN** — WireGuard / Tailscale — Secure remote access to homelab  

**Network layout:** lab VMs and containers sit behind OPNsense, split into VLANs. Proxmox management, cluster traffic and the NAS stay on the house network, so an OPNsense outage can't lock me out of the hypervisor. A dedicated management VLAN (with a backup way in) can come later once things are stable.

### 🟠 Phase 2 — Dashboards & Entry Points

- **Dashboard** — Homarr — Full-featured service dashboard  
- **Dashboard** — Glance — Lightweight status dashboard  
- **Dashboard** — Homepage — Central service overview  
- **Monitoring & Uptime** — Uptime Kuma — Service availability tracking  

### 🟡 Phase 3 — Backups, Storage & Personal Data Layer

- **Backup System** — Duplicati / Restic / Kopia — Encrypted 3-2-1 backups, set up and restore-tested before any real data goes in  
- **Photo Storage** — Immich — Self-hosted photo backup and management  
- **Document Management** — Paperless-ngx — OCR document storage system  
- **File Management** — Filebrowser — Web-based file access for NAS storage  
- **Password Management** — Vaultwarden — Secure password vault  

### 🟢 Phase 4 — Media Services (Video, Music, Audio)

- **Video Streaming** — Jellyfin — Media server for video, TV, and movies  
- **Music Streaming Server** — Navidrome — Self-hosted Spotify-like music server  
- **Music Client** — Feishin — Web player for Navidrome  
- **Audiobook Server** — Audiobookshelf — Audiobook and podcast management  

### 🔵 Phase 5 — Updates & System Management

- **Container Update Alerts** — Watchtower (notify-only) / Diun — Flags new images; Immich updated by hand after reading release notes  
- **Docker Management** — Dockge / Portainer — Container management UI  
- **Workflow Automation** — Node-RED — System automation and integrations  

### ⚪ Phase 6 — Observability & Metrics

- **Metrics Collection** — Prometheus — System metrics backend  
- **Dashboards** — Grafana — Visual monitoring and analytics  

## Tasks (Project Roadmap)

- Create a full homelab architecture diagram (Proxmox → services → NAS → network flow)  
- Decide on a primary dashboard system (Homarr vs Glance vs Homepage)  
- Standardise service deployment structure (Docker Compose per phase)  
- Implement Phase 1 infrastructure services (DNS, VPN, Proxmox setup)  
- Begin deploying Phase 2 services (dashboards + monitoring)  
- Establish consistent naming conventions across all services  
- Document configurations for reproducibility and learning  