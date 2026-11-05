# Configuraciones de los routers

Transcritas de las capturas tomadas durante el montaje (`../img/Router_*.png`).

| Fichero | Ruta en el router | Para qué |
|---|---|---|
| `rou10/interfaces` | `/etc/network/interfaces` | IP de las dos patas y rutas estáticas a las subredes 11-15 |
| `rou10/kea-dhcp4.conf` | `/etc/kea/kea-dhcp4.conf` | DHCP de la subred 192.168.10.0/24 |
| `rou10/nftables.conf` | `/etc/nftables.conf` | NAT (masquerading) hacia internet |
| `rou10/99-ip_forward.conf` | `/etc/sysctl.d/99-ip_forward.conf` | Activa el enrutamiento |
| `rou10/sources.list` | `/etc/apt/sources.list` | Repositorios de Debian 13 |
| `rou11/interfaces` | `/etc/network/interfaces` | Router clonado: pata en la 10 y red propia en la 11 |

Rou12 a Rou15 siguen el mismo patrón que Rou11 cambiando el tercer octeto. En Kea y nftables de cada clon se sustituye `192.168.10.x` por `192.168.1X.x` de su subred.
