# 🎨 Recursos Visuales y Badges

Este documento contiene recursos adicionales para mejorar la presentación del proyecto.

## 🏷️ Badges Adicionales

### Tecnologías

```markdown
![Proxmox](https://img.shields.io/badge/Proxmox-VE_8.x-E57000?style=for-the-badge&logo=proxmox&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)
![Kong](https://img.shields.io/badge/Kong-003459?style=for-the-badge&logo=kong&logoColor=white)
![n8n](https://img.shields.io/badge/n8n-EA4B71?style=for-the-badge&logo=n8n&logoColor=white)
![Metabase](https://img.shields.io/badge/Metabase-509EE3?style=for-the-badge&logo=metabase&logoColor=white)
```

### Estado del Proyecto

```markdown
![Status](https://img.shields.io/badge/Status-Production-success?style=for-the-badge)
![Uptime](https://img.shields.io/badge/Uptime-99.9%25-brightgreen?style=for-the-badge)
![Maintained](https://img.shields.io/badge/Maintained-Yes-green?style=for-the-badge)
```

### Métricas

```markdown
![Services](https://img.shields.io/badge/Services-11+-blue?style=for-the-badge)
![Containers](https://img.shields.io/badge/LXC_Containers-3-orange?style=for-the-badge)
![VLANs](https://img.shields.io/badge/VLANs-5-purple?style=for-the-badge)
```

## 🎨 Iconos para Secciones

### Emojis Útiles

| Categoría | Emoji | Uso |
|:----------|:------|:----|
| **Infraestructura** | 🏢 🖥️ ⚡ | Servidores, hardware |
| **Red** | 🌐 🔌 📡 | Networking, conectividad |
| **Seguridad** | 🔒 🛡️ 🔐 | Seguridad, autenticación |
| **Datos** | 💾 📊 📈 | Bases de datos, analytics |
| **Automatización** | ⚙️ ⚡ 🔄 | Workflows, procesos |
| **IA** | 🧠 🤖 🎯 | Machine learning, AI |
| **Monitoreo** | 📊 👁️ 📉 | Observabilidad, métricas |
| **Documentación** | 📖 📝 📋 | Docs, guías |
| **Desarrollo** | 💻 🔧 🛠️ | Dev tools, utilities |

## 📊 Diagramas Mermaid - Temas de Color

### Tema Actual (Colorido)
```mermaid
%%{init: {'theme':'default'}}%%
```

### Tema Oscuro
```mermaid
%%{init: {'theme':'dark'}}%%
```

### Tema Neutral
```mermaid
%%{init: {'theme':'neutral'}}%%
```

## 🎨 Paleta de Colores del Proyecto

### Colores Principales

| Color | Hex | Uso |
|:------|:----|:----|
| **Azul Proxmox** | `#E57000` | Infraestructura |
| **Verde Éxito** | `#2e7d32` | Estados positivos |
| **Rojo Alerta** | `#c2185b` | Alertas, crítico |
| **Púrpura** | `#6a1b9a` | Automatización |
| **Azul Datos** | `#1565c0` | Datos, analytics |

### Gradientes Sugeridos

```css
/* Gradiente Principal */
background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);

/* Gradiente Datos */
background: linear-gradient(135deg, #1565c0 0%, #2e7d32 100%);

/* Gradiente Seguridad */
background: linear-gradient(135deg, #c2185b 0%, #6a1b9a 100%);
```

## 📸 Guía de Screenshots

### Configuración Recomendada

- **Resolución:** 1920x1080 o superior
- **Formato:** PNG (mejor calidad) o WebP (menor tamaño)
- **Herramienta:** Flameshot, Spectacle, o similar
- **Edición:** Blur para información sensible

### Checklist Pre-Upload

- [ ] Información sensible censurada
- [ ] Resolución adecuada
- [ ] Nombre descriptivo
- [ ] Tamaño optimizado (< 500KB si es posible)

### Comando para Optimizar PNGs

```bash
# Instalar optipng
sudo apt install optipng

# Optimizar imagen
optipng -o7 screenshot.png
```

## 🎬 Animaciones y GIFs

### Crear GIF desde Grabación de Pantalla

```bash
# Instalar herramientas
sudo apt install peek

# O usando ffmpeg
ffmpeg -i input.mp4 -vf "fps=10,scale=1280:-1:flags=lanczos" -c:v gif output.gif
```

### Optimizar GIFs

```bash
# Instalar gifsicle
sudo apt install gifsicle

# Optimizar
gifsicle -O3 --colors 256 input.gif -o output.gif
```

## 🔗 Enlaces Útiles

### Generadores de Badges
- [Shields.io](https://shields.io/) - Generador principal de badges
- [Simple Icons](https://simpleicons.org/) - Iconos para badges
- [Badge Generator](https://badgen.net/) - Alternativa a Shields.io

### Herramientas de Diagramas
- [Mermaid Live Editor](https://mermaid.live/) - Editor en vivo de Mermaid
- [Draw.io](https://app.diagrams.net/) - Diagramas más complejos
- [Excalidraw](https://excalidraw.com/) - Diagramas estilo sketch

### Recursos de Diseño
- [Coolors](https://coolors.co/) - Generador de paletas de colores
- [Unsplash](https://unsplash.com/) - Imágenes de alta calidad
- [Heroicons](https://heroicons.com/) - Iconos SVG

---

**Última actualización:** 2026-01-30  
**Mantenido por:** DevLewiso
