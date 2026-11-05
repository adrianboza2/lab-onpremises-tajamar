# Diagrama de red del lab

```mermaid
flowchart TB
    INET((Internet))
    NAT[VMware NAT]
    INET --- NAT

    subgraph V10["VMnet10 · 192.168.10.0/24"]
        R10["Rou10 · Debian<br/>ens32: DHCP (NAT)<br/>ens33: 192.168.10.1<br/>Kea DHCP · nftables NAT"]
        W10["Cliente W11<br/>DHCP .100-.200"]
    end
    NAT --- R10
    R10 --- W10

    subgraph V11["VMnet11 · 192.168.11.0/24"]
        R11["Rou11 · Debian<br/>ens32: 192.168.10.11<br/>ens33: 192.168.11.1"]
        DC["WS25DC · Windows Server 2025<br/>192.168.11.2<br/>AD DS + DNS · mss.loc"]
        W11["Clientes W11<br/>unidos a mss.loc"]
    end
    R10 -- "ruta 192.168.11.0/24 via .10.11" --- R11
    R11 --- DC
    R11 --- W11
    DC -. "DNS / autenticación" .- W11

    R1X["Rou12 … Rou15<br/>ens32: 192.168.10.1X<br/>ens33: 192.168.1X.1"]
    R10 -- "rutas 192.168.12-15.0/24" --- R1X
```

| Equipo | Red | IP | Función |
|---|---|---|---|
| Rou10 | NAT + VMnet10 | DHCP / 192.168.10.1 | Router de borde, DHCP, NAT |
| Rou11…Rou15 | VMnet10 + VMnet1X | 192.168.10.1X / 192.168.1X.1 | Router de cada subred |
| WS25DC | VMnet11 | 192.168.11.2 | Controlador de dominio y DNS de `mss.loc` |
| Clientes W11 | VMnet10 / VMnet11 | DHCP | Pruebas y equipos del dominio |
