<div align="center">

# 🏠 Homelab Architecture

<img src="https://img.shields.io/badge/Status-Active-success?style=for-the-badge" alt="Status">
<img src="https://img.shields.io/badge/Proxmox-VE-orange?style=for-the-badge&logo=proxmox" alt="Proxmox">
<img src="https://img.shields.io/badge/License-MIT-blue?style=for-the-badge" alt="License">

**Documentación de mi homelab con diagramas de red y arquitectura de servicios**

[📊 Topología](#️-topología-de-red) • [🏗️ Arquitectura](#️-arquitectura-de-servicios) • [📖 Segmentación](#-segmentación-de-red)

</div>

---

## 📋 Contenido

- [🗺️ Topología de Red](#️-topología-de-red)
- [🏗️ Arquitectura de Servicios](#️-arquitectura-de-servicios)
- [📊 Segmentación de Red](#-segmentación-de-red)
- [📖 Documentación](#-documentación)

---

## 🗺️ Topología de Red

Infraestructura de red física del homelab con **The Matrix** como router principal y **Oracle** como switch core.

```mermaid
graph TB
    subgraph Internet["🌍 Internet"]
        WAN1[("WAN<br/>1000FDX")]
    end
    
    subgraph Core["🔷 Core Network"]
        Matrix["The Matrix<br/>Router Principal"]
        Oracle["Oracle Switch<br/>1000FDX"]
    end
    
    subgraph ClientZone["👥 Zona de Clientes"]
        ClientGroup1["Client Group<br/>16 dispositivos"]
        ClientGroup2["Client Group<br/>9 dispositivos"]
    end
    
    subgraph Management["⚙️ Gestión"]
        OmadaCtrl["Omada Controller"]
    end
    
    subgraph Surveillance["📹 Vigilancia"]
        CameraGroup["Cámaras IP<br/>3 dispositivos"]
    end
    
    subgraph Servers["🖥️ Servidores"]
        NetworkMonitor["Network Monitor"]
        CasaOS["CasaOS Media Server"]
        ProxmoxSrv["Proxmox Server<br/>Ryzen 7 5700G"]
        NVR["NVR Server"]
    end
    
    %% Conexiones principales
    WAN1 -->|"Fibra"| Matrix
    Matrix -->|"Trunk"| Oracle
    
    %% Distribución
    Oracle --> ClientGroup1
    Oracle --> ClientGroup2
    Oracle --> CameraGroup
    Oracle --> OmadaCtrl
    
    %% Servidores
    ClientGroup2 -.-> NetworkMonitor
    ClientGroup2 -.-> CasaOS
    ClientGroup2 -.-> ProxmoxSrv
    ClientGroup2 -.-> NVR
    
    %% Estilos
    classDef internetStyle fill:#e1f5ff,stroke:#01579b,stroke-width:3px
    classDef coreStyle fill:#fff3e0,stroke:#e65100,stroke-width:3px
    classDef clientStyle fill:#f3e5f5,stroke:#4a148c,stroke-width:2px
    classDef serverStyle fill:#e8f5e9,stroke:#1b5e20,stroke-width:2px
    classDef mgmtStyle fill:#fce4ec,stroke:#880e4f,stroke-width:2px
    
    class WAN1 internetStyle
    class Matrix,Oracle coreStyle
    class ClientGroup1,ClientGroup2 clientStyle
    class NetworkMonitor,CasaOS,ProxmoxSrv,NVR serverStyle
    class OmadaCtrl,CameraGroup mgmtStyle
```

---

## 🏗️ Arquitectura de Servicios

### Stack de Datos (10.0.0.60)

Servicios de BI y gestión de datos corriendo en contenedores Docker.

```mermaid
graph LR
    subgraph Gateway_Layer["🛡️ Capa de Acceso (IP .58)"]
        Kong[Kong API Gateway]
    end

    subgraph Data_Stack_Container["📊 Stack de Datos & BI (IP .60)"]
        direction TB
        MB[📈 Metabase]
        NC[📑 NocoDB]
        DIR[🚀 Directus]
        DB[(🐘 PostgreSQL)]

        %% Conexiones internas a la DB
        MB -.->|Port 5432| DB
        NC -.->|Port 5432| DB
        DIR -.->|Port 5432| DB
    end

    %% Flujos desde el Gateway
    User((Usuario)) ==>|Acceso Seguro| Kong
    
    Kong ==>|Ruta: /bi <br/> Port 3000| MB
    Kong ==>|Ruta: /tablas <br/> Port 8080| NC
    Kong ==>|Ruta: /cms <br/> Port 8055| DIR

    style Data_Stack_Container fill:#f9f9f9,stroke:#333,stroke-width:2px
    style DB fill:#336791,color:#fff
    style Kong fill:#003366,color:#fff
```

---

## 📊 Segmentación de Red

Plan de direccionamiento IP por función y propósito.

| Rango | Propósito |
|:------|:----------|
| **10.0.0.1 – 9** | Gateway / Firewall |
| **10.0.0.10 – 19** | Core / Infra |
| **10.0.0.20 – 29** | Dev / Staging interno |
| **10.0.0.30 – 39** | Observabilidad / Seguridad |
| **10.0.0.50 – 69** | Servicios base (DevOps / acceso) |
| **10.0.0.70 – 99** | Apps públicas |
| **10.0.0.100 – 199** | Media / Usuario |
| **10.0.0.200 – 229** | Automatización / IoT |
| **10.0.0.230 – 254** | IA / Labs / Experimentos |

---

## 📖 Documentación

### Estructura del Repositorio

```
homelab-architecture/
│
├── README.md                    # Este archivo
├── diagrams/                    # Diagramas fuente Mermaid
├── docs/                        # Documentación adicional
├── screenshots/                 # Capturas de pantalla
└── configs/                     # Configuraciones de ejemplo
```

---

## 👨‍💻 Autor

**DevLewiso**

- GitHub: [@devlewiso](https://github.com/devlewiso)

---

<div align="center">

Hecho con ❤️ para documentar mi homelab

</div>
