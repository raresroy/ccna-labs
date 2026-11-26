# Habilidades practicadas en el laboratorio

## 1. Diseño y direccionamiento de red
- Diseño jerárquico de tres capas: acceso (ACC-1 a ACC-6), distribución y núcleo (SW-CORE-FIEE).
- Segmentación por VLAN: 10, 20, 30, 50, 60, 70, 80 y 100, cada una con su subred /24.
- Planificación de direccionamiento IPv4 para sede principal, DMZ (172.16.100.0/24) y sede remota (10.20.x.x).
- Uso de sumarización de redes (10.10.0.0/16) y de máscaras wildcard en ACL.

## 2. Conmutación (Capa 2)
- Creación y asignación de VLAN a puertos de acceso.
- Configuración de enlaces troncales 802.1Q entre switches.
- Agregación de enlaces con EtherChannel:
  - LACP (estándar IEEE 802.3ad): po1 y po2.
  - PAgP (propietario de Cisco): po3.
- Comparación entre protocolos de agregación y verificación del estado de los canales.

## 3. Enrutamiento y alta disponibilidad (Capa 3)
- Enrutamiento dinámico con OSPF entre los routers internos y el perimetral.
- Propagación de la ruta por defecto con `default-information originate`.
- Redundancia del gateway con HSRP (IP virtual .1) en Router0 y Router0(1).
- Configuración de enlaces seriales (WAN) con `clock rate` en el extremo DCE.
- Configuración de rutas estáticas y de la ruta por defecto hacia Internet.

## 4. Servicios de red
- Servidor DHCP centralizado en la VLAN80 con relay (`ip helper-address`) para las demás VLAN.
- Publicación de servicios en la DMZ: Web, DNS y Correo.
- Resolución de nombres con DNS (matricula.uni.edu.pe).

## 5. Seguridad en la capa de acceso (Fase 12)
- **DHCP Snooping**
  - Clasificación de puertos en trusted y untrusted.
  - Mitigación de servidores DHCP falsos (rogue DHCP) y de ataques de agotamiento (starvation).
  - Limitación de tasa de paquetes con `ip dhcp snooping limit rate`.
  - Interpretación de la binding table (IP, MAC, VLAN, puerto).
  - Uso de `no ip dhcp snooping information option` para evitar descartes por Option 82.
- **Dynamic ARP Inspection (DAI)**
  - Validación de paquetes ARP contra la binding table.
  - Mitigación de ARP spoofing/poisoning.
  - Validación de `src-mac`, `dst-mac` e `ip`.
  - Manejo de hosts con IP estática mediante `ip source binding` o ARP ACL.
- Recuperación de puertos en estado err-disable (`errdisable recovery`).

## 6. NAT y seguridad perimetral (Fase 13)
- Identificación de interfaces `ip nat inside` e `ip nat outside` en Router0(2).
- **PAT (overload)** para que las VLAN internas salgan a Internet con una sola IP pública.
- **NAT estático 1:1** y **port forwarding** para publicar los servidores de la DMZ.
- Definición del tráfico a traducir con ACL estándar.
- Filtrado de tráfico entrante desde Internet con ACL extendida nombrada (`OUTSIDE-IN`).
- Comprensión de que la ACL de entrada se evalúa antes del NAT (usa IP públicas).
- Diseño de una DMZ separada de la red interna.
- Replicación del esquema NAT en la sede remota (RT-NICTEL).

## 7. Verificación y resolución de problemas
- Comandos de verificación:
  - `show ip interface brief`
  - `show ip route`
  - `show ip nat translations` y `show ip nat statistics`
  - `show ip dhcp snooping` y `show ip dhcp snooping binding`
  - `show ip arp inspection`
  - `show controllers` (identificación del DCE)
  - `show cdp neighbors`
- Pruebas funcionales: ping extremo a extremo, renovación DHCP, acceso a servicios publicados desde la sede remota.
- Diagnóstico de fallas comunes: enlaces seriales caídos por falta de clock rate, puertos bloqueados por rate limit, ACL que bloquea el retorno del tráfico.

## 8. Herramientas y buenas prácticas
- Simulación y documentación de la topología en Cisco Packet Tracer.
- Uso de descripciones en interfaces y nombres de host claros.
- Respaldo de configuraciones con `write memory`.
- Aplicación gradual de cambios: primero funcionalidad, luego restricciones (ACL).
- Documentación técnica del laboratorio por fases.