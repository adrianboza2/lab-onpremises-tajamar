# 04 · Operación del lab (aula y casa)

Las VMs viven en un **disco duro portátil** (`E:\lab\`) y se abren desde ahí tanto en el aula como en casa. Así hay una única copia de cada máquina.

## Reglas

1. **Apagar del todo, nunca suspender**, antes de sacar el disco. Una VM encendida o suspendida se corrompe al desenchufar.
2. **Expulsión segura** del disco.
3. Al abrir la VM en otro PC, responder **"I Moved It"**: conserva UUID y MAC. "I Copied It" genera una identidad nueva y la red del lab deja de cuadrar.
4. Una sola copia canónica: la del disco.

## Red entre VMs en distintos PCs

Las VMnets y los *LAN Segments* son de cada PC, no viajan con la VM: hay que crearlos con **el mismo nombre** en cada equipo donde se abra el lab.

## Ahorro de espacio

Rellenar con ceros el espacio libre dentro de la VM y luego **Compact** del disco en VMware (o `vmware-vdiskmanager -k`).
