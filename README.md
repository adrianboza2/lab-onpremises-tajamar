# Lab on-premises: red enrutada con Debian y dominio Active Directory

Laboratorio de infraestructura on-premises montado en VMware durante el Tema 01 (On Premises, módulos M1-M3) del Máster en Ciberseguridad Cloud/DevSecOps de Tajamar Tech (2026-2027).

Es la base sobre la que crecerá el proyecto del máster: primero la red y la identidad en local y, en los siguientes módulos, su extensión a la nube (Azure), la automatización con IaC y el bastionado.

## Objetivo

Montar desde cero una red corporativa pequeña y documentarla para poder reproducirla:

- Routers Linux (Debian) que dan salida a internet con NAT, reparten IP por DHCP y enrutan entre varias subredes.
- Un controlador de dominio Windows Server 2025 (`mss.loc`) con usuarios, grupos, carpetas compartidas con permisos por departamento y directivas de grupo (GPO).
- Clientes Windows 11 unidos al dominio.

## Tecnologías

| Área | Tecnología |
|---|---|
| Virtualización | VMware Workstation (clones enlazados, VMnets / LAN Segments) |
| Routers | Debian 13 (trixie), `ifupdown`, `nftables` (NAT por masquerading), `sysctl` (ip_forward), rutas estáticas |
| DHCP | ISC Kea (`kea-dhcp4-server`) |
| Acceso remoto | OpenSSH |
| Identidad | Windows Server 2025 Standard (Desktop Experience), Active Directory Domain Services, DNS, GPO |
| Clientes | Windows 11 con TPM virtual y arranque seguro |

## Alcance inicial (versión 0.1)

Incluido en esta versión:

1. **Red**: router `Rou10` con salida a internet y routers `Rou11`…`Rou15` clonados, cada uno con su subred `192.168.1X.0/24` y enrutamiento entre todas ellas. → [docs/01-router-debian-kea.md](docs/01-router-debian-kea.md)
2. **Dominio**: Windows Server 2025 promovido a controlador de dominio de `mss.loc`, con OU, 6 usuarios en 3 departamentos, carpetas con permisos NTFS y GPO. → [docs/02-windows-server-ad-ds.md](docs/02-windows-server-ad-ds.md)
3. **Clientes**: plantilla de Windows 11 y su unión al dominio. → [docs/03-cliente-windows-11.md](docs/03-cliente-windows-11.md)
4. **Operación del lab**: cómo se guarda y se mueve entre el aula y casa. → [docs/04-operacion-del-lab.md](docs/04-operacion-del-lab.md)
5. **Configuraciones** reales de los routers en [`configs/`](configs/) y el **diagrama de red** en [`diagramas/`](diagramas/red.md).

Fuera de alcance por ahora (siguientes fases, ver [ROADMAP.md](ROADMAP.md)): bastionado, conexión con Azure, automatización con IaC y monitorización.

## Estructura del repositorio

```
.
├── README.md
├── ROADMAP.md            # fases siguientes del proyecto
├── docs/                 # guías paso a paso de cada pieza
├── configs/              # ficheros de configuración de los routers
│   ├── rou10/
│   └── rou11/
├── diagramas/            # diagrama de red (Mermaid)
└── img/                  # capturas tomadas durante el montaje
```

## Aviso

Es un laboratorio de aprendizaje. Algunas decisiones (root por SSH con contraseña, complejidad de contraseñas desactivada por GPO) se tomaron para agilizar las prácticas y **no son válidas en producción**. Están señaladas en cada guía y su corrección forma parte del roadmap.

## Autor

**Adrián Boza Suárez** · [github.com/adrianboza2](https://github.com/adrianboza2)
Máster en Ciberseguridad Cloud/DevSecOps · Tajamar Tech · 2026-2027
