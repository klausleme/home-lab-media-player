# Home Lab Media Server Infrastructure

![Oracle Cloud](https://img.shields.io/badge/Oracle_Cloud-F80000?style=for-the-badge&logo=oracle&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black)
![Tailscale](https://img.shields.io/badge/Tailscale-18181B?style=for-the-badge&logo=tailscale&logoColor=white)

Repositório contendo a infraestrutura como código (IaC) do meu servidor doméstico. O foco é automação, segurança, eficiência energética e gerenciamento de mídia via Docker.

## 🏗️ Arquitetura do Sistema

```mermaid
graph TD
    User((Usuário Remoto)) -->|VPN Segura| TS[Tailscale/ZeroTier]
    TS -->|Túnel Criptografado| Server[Home Server Ubuntu]
    
    subgraph "Docker Host"
        Server -->|Gerencia| PlexStack[Plex Container]
        Server -->|Gerencia| ArrStack[Arr Suite & Downloaders]
    end
    
    subgraph "Storage & Hardware"
        PlexStack -->|Leitura| HDD[HD Externo Hitachi]
        ArrStack -->|Atomic Moves/Hardlinks| HDD
        OS[OS] -->|hd-idle| HDD
    end
    
    classDef security fill:#f9f,stroke:#333,stroke-width:2px;
    class TS security;
