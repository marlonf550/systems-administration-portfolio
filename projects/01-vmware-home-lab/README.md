# 01 — VMware Home Lab

[Português](#português) | [English](#english)

## Português

### Objetivo

Documentar o ambiente VMware que suporta este portfólio: capacidade, segmentação lógica, operação segura e serviços reutilizáveis.

### Estado e pressupostos

- Plataforma: VMware — edição e versão `TBD`.
- Hardware, datastore, switches virtuais e redes: `TBD`.
- IPs públicos, credenciais e identificadores de ativos não são publicados.

### Arquitetura

```mermaid
flowchart TB
  ADMIN["Administrador"]
    PHYS["Host físico<br/>VMware ESXi 8<br/>64 GB RAM"]
    ADMIN -->|HTTPS / vSphere Client| VC

    subgraph NESTED["Laboratório de virtualização"]
        PHYS
        N1["ESXi-N1<br/>Hipervisor aninhado"]
        N2["ESXi-N2<br/>Hipervisor aninhado"]
        VC["vCenter Server<br/>Gestão centralizada"]
        AD["AD / DNS / DHCP"]
        APP["Máquinas virtuais<br/>de teste"]
        VEEAM["Veeam Server"]
        MON["Zabbix / ferramentas"]
        PHYS --> N1
        PHYS --> N2
        N1 --> VC
        N1 --> AD
        N1 --> APP
        N2 --> VEEAM
        N2 --> MON
    end

    subgraph NETWORKS["Redes lógicas"]
        MGMT["VLAN 10 — Management<br/>172.20.10.0/24"]
        STORAGE["VLAN 20 — Storage<br/>172.20.20.0/24"]
        SERVERS["VLAN 30 — Servers<br/>172.20.30.0/24"]
        DMZ["VLAN 40 — DMZ<br/>Subnet a definir"]
    end

    N1 -. "Gestão" .-> MGMT
    N2 -. "Gestão" .-> MGMT
    AD -. "Serviços" .-> SERVERS
    APP -. "Serviços" .-> SERVERS
    VEEAM -. "Backup" .-> SERVERS
    PHYS -. "Tráfego de storage" .-> STORAGE
    APP -. "Serviços expostos controlados" .-> DMZ

    NAS["TrueNAS / Storage<br/>preferencialmente fora<br/>dos ESXi aninhados"]
    NAS --- STORAGE
```

### Implementação e validação

1. Registar host, capacidade e versão no [inventário](../../docs/lab-inventory.md).
2. Definir convenção de nomes para VMs, redes e snapshots.
3. Separar gestão, serviços e laboratório em grupos de portas/redes, quando aplicável.
4. Documentar templates de VM atualizados e com hardening básico.
5. Validar acesso de gestão, conectividade autorizada e espaço disponível.

**Evidência a adicionar:** captura redigida da consola; tabela de VMs sem dados sensíveis; teste de restauração; registo de capacidade.

## English

### Objective

Document the VMware environment supporting this portfolio: capacity, logical segmentation, secure operations, and reusable services.

### Summary

Inventory the host and workloads, standardize naming, segment management and service networks where applicable, maintain hardened VM templates, and validate management access, authorized connectivity, and available capacity. Product/version, host details, storage, and networks remain `TBD` until verified.

