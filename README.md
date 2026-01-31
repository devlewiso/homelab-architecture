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
graph TD
    %% Estilos de hardware Omada
    classDef router fill:#2c3e50,stroke:#1abc9c,stroke-width:2px,color:#fff
    classDef switch fill:#34495e,stroke:#3498db,stroke-width:2px,color:#fff
    classDef device fill:#ecf0f1,stroke:#bdc3c7,color:#2c3e50
    classDef group fill:#7f8c8d,stroke:#95a5a6,color:#fff

    %% Nivel de Entrada
    WAN1((Internet)) --- TheMatrix["ER605: The Matrix<br/>10.0.0.1"]:::router

    %% Distribución Core
    TheMatrix --- Oracle["SG3428: Oracle 🐙<br/>10.0.0.10"]:::switch
    TheMatrix --- Controller["Omada Controller<br/>10.0.0.11"]:::device

    %% Grupos de Red
    Oracle --- ClientGroup1[Client Group]:::group
    Oracle --- ClientGroup2[Client Group]:::group
    Oracle --- CameraGroup[Camera Group]:::group

    %% Dispositivos - Client Group (Rama 1 - Infraestructura)
    subgraph Clients_A [Infraestructura de Red]
        S1["Network Monitor Server<br/>10.0.0.30"]:::device
        S2["CasaOS Media Server<br/>10.0.0.100"]:::device
        S3["Proxmox Server<br/>10.0.0.12"]:::device
        S4["NVR Server<br/>10.0.0.31"]:::device
        S5["Personal Laptop<br/>10.0.0.101"]:::device
        S6["Workstation<br/>10.0.0.102"]:::device
    end
    ClientGroup1 --- Clients_A

    %% Dispositivos - Client Group (Rama WiFi/Personal)
    subgraph Clients_B [Dispositivos de Usuario]
        D1["HUAWEI_MatePad<br/>10.0.0.103"]:::device
        D2["EchoOficina<br/>10.0.0.200"]:::device
        D3["Celular<br/>10.0.0.104"]:::device
        D4["deco-X55<br/>10.0.0.13"]:::device
        D5["Google-Home<br/>10.0.0.201"]:::device
        D6["Celular1<br/>10.0.0.105"]:::device
        D7["My HP Laptop<br/>10.0.0.106"]:::device
        D8["Celular2<br/>10.0.0.107"]:::device
        D9["Google-Nest-Mini<br/>10.0.0.202"]:::device
    end
    ClientGroup2 --- Clients_B

    %% Dispositivos - Camera Group (EZVIZ)
    subgraph Cameras [Cámaras de Seguridad]
        C1["Doorbell Camera<br/>10.0.0.32"]:::device
        C2["backyard Camera<br/>10.0.0.33"]:::device
        C3["Garage Camera<br/>10.0.0.34"]:::device
        C4["HomeLab Camera<br/>10.0.0.35"]:::device
    end
    CameraGroup --- Cameras
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
