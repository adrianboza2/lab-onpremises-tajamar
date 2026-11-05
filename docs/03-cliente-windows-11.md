# 03 · Cliente Windows 11 (plantilla)

Se crea una plantilla y de ella salen los clientes del lab mediante clones enlazados.

## Crear la VM en VMware

- Configuración **personalizada** e "instalar el SO después".
- **TPM virtual** (cifrado ligado al hardware) y **arranque seguro**, que Windows 11 exige.

## Ajustes tras instalar

- VMware Tools.
- `Set-ExecutionPolicy` para poder lanzar los scripts del aula: uno que habilita el ping (ICMPv4) en el firewall y otro que pone el teclado en español a todos los usuarios.
- Plan de energía sin suspensión, para que las VMs no se duerman.
- Actualizar, quitar software sobrante y, en VMware, **desfragmentar y compactar** el disco.

## Clonar

- Siempre **clon enlazado**: ocupa poco y sale en segundos.
- **Siempre cambiar la MAC** al clonar. Si no, Kea da la misma IP a dos equipos.

## Unir al dominio

DNS apuntando al controlador de dominio (`192.168.11.2`) y unir a `mss.loc` con credenciales de administrador del dominio. Detalle en [02-windows-server-ad-ds.md](02-windows-server-ad-ds.md#4-unir-un-cliente-al-dominio).
