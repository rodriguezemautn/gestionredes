
## 🧪 **EXPERIENCIAS PRÁCTICAS EN CLASE**

### ** EXPERIENCIA PRÁCTICA: "PRIMER CONTACTO CON RB951-2HnD"**

#### ** Objetivos:**
- Familiarizarse físicamente con el hardware RouterBoard
- Realizar configuración inicial desde factory reset
- Establecer múltiples métodos de acceso
- Documentar proceso de troubleshooting inicial

#### ** Materiales por Grupo:**
- 1 Router MikroTik RB951-2HnD
- 1 PC/Laptop con Winbox y navegador
- 2 cables Ethernet
- 1 fuente PoE o adaptador de corriente
- Cronómetro para medir tiempos

#### ** Setup Físico:**
```
[PC Grupo X] ───── Cable Ethernet ───── [ether2 RB951-2HnD ether1] ───── [Switch Central]
                                              │
                                         [LED Status]
```

#### **📋 Procedimiento Detallado:**

**Paso 1: Análisis Físico (10 minutos)**
```bash
# Documentar en planilla:
- Identificar 5 puertos Ethernet (ether1-ether5)
- Localizar botón de reset
- Identificar LEDs de estado
- Verificar etiqueta con MAC address y modelo
- Medir consumo eléctrico con multímetro (si disponible)
```

**Paso 2: Factory Reset y Boot Analysis (15 minutos)**
```bash
# Cronometrar proceso completo:
1. Desconectar alimentación
2. Mantener botón reset presionado
3. Conectar alimentación (mantener reset 10 seg)
4. Observar secuencia de LEDs
5. Cronometrar tiempo total de boot

# Documentar:
- Tiempo total de reset: _____ segundos
- Secuencia de LEDs observada: _____________
- IP por defecto asignada: _______________
```

**Paso 3: Multi-Access Configuration (20 minutos)**
```bash
# A. Acceso via Winbox
/system identity set name="RB951-Grupo-[X]"
/system clock set time-zone-name=America/Argentina/Buenos_Aires

# B. Configurar acceso web
/ip service set www disabled=no port=80
/ip service set www-ssl disabled=no port=443

# C. Configurar SSH
/ip service set ssh disabled=no port=22
/user set admin password="Lab2024!"

# D. Verificar todos los accesos
# Documentar cual funciona mejor y por qué
```

**Paso 4: Network Interface Analysis (25 minutos)**
```bash
# Configuración de interfaces
/interface ethernet set ether1 name="WAN-Lab"
/interface ethernet set ether2 name="LAN-PC"
/interface ethernet set ether3 name="LAN-Test1"
/interface ethernet set ether4 name="LAN-Test2"
/interface ethernet set ether5 name="LAN-Expansion"

# Asignación de IPs
/ip address add address=10.10.[X].1/24 interface=LAN-PC comment="Red del Grupo [X]"
/ip address add address=192.168.100.[X]/24 interface=WAN-Lab comment="Red de Laboratorio"

# Testing de conectividad
/ping 192.168.100.1 count=5 size=1500
/ping 192.168.100.1 count=5 size=64

# Documentar:
# - Tiempo de respuesta promedio con paquetes pequeños: _____ ms
# - Tiempo de respuesta promedio con paquetes grandes: _____ ms
# - Diferencia observada: _____ ms
```

**Paso 5: Basic Performance Testing (15 minutos)**
```bash
# Test de throughput básico
/tool bandwidth-test address=192.168.100.1 duration=10s direction=both

# Monitoreo de recursos
/system resource print
/system resource monitor duration=30s

# Documentar:
# - CPU usage durante test: _____ %
# - Memory utilization: _____ %
# - Throughput TCP upload: _____ Mbps
# - Throughput TCP download: _____ Mbps
```

#### **Análisis y Documentación Requerida:**

**Planilla de Resultados Grupo [X]:**
```
┌─────────────────────────────────────────────────────────┐
│              LABORATORIO                                │
│            Análisis RouterBoard RB951-2HnD              │
├─────────────────────────────────────────────────────────┤
│ 1. HARDWARE ANALYSIS                                    │
│    MAC Address: ________________________               │
│    Serial Number: ______________________               │
│    Boot Time: _________ segundos                        │
│    LED Sequence: _______________________                │
│                                                         │
│ 2. ACCESS METHODS                                       │
│    Winbox Speed (subjetivo 1-10): ____                  │
│    WebFig Speed (subjetivo 1-10): ____                  │
│    SSH Responsiveness (1-10): ____                      │
│    Método preferido: _______________                     │
│    Justificación: _______________________               │
│                                                         │
│ 3. NETWORK PERFORMANCE                                  │
│    Ping 64 bytes average: ______ ms                     │
│    Ping 1500 bytes average: ______ ms                   │
│    TCP Upload: ______ Mbps                              │
│    TCP Download: ______ Mbps                            │
│                                                         │
│ 4. RESOURCE UTILIZATION                                 │
│    Idle CPU: ______ %                                   │
│    Under load CPU: ______ %                             │
│    Memory usage: ______ %                               │
│                                                         │
│ 5. OBSERVATIONS & ISSUES                                │
│    Problems encountered: ___________________            │
│    Solutions applied: _______________________           │
│    Improvement suggestions: _________________           │
└─────────────────────────────────────────────────────────┘
```

---

### ** EXPERIENCIA PRÁCTICA: "STATIC ROUTING CHAIN TOPOLOGY"**

#### **🎯 Objetivos:**
- Implementar routing estático en topología lineal con 6 routers
- Analizar tabla de rutas y proceso de forwarding
- Medir impacto de multiple hops en latencia
- Troubleshoot conectividad end-to-end

#### **🔧 Setup Físico:**
```
[PC1] ── [RB951-1] ── [RB951-2] ── [RB951-3] ── [RB951-4] ── [RB951-5] ── [RB951-6] ── [PC6]
   │    10.1.1.0/30  10.1.2.0/30  10.1.3.0/30  10.1.4.0/30  10.1.5.0/30    │
   │                                                                         │
192.168.1.0/24                                                       192.168.6.0/24
```

#### **📋 Procedimiento por Router:**

**Router 1 (Grupo 1):**
```bash
# Reset y configuración base
/system reset-configuration no-defaults=yes skip-backup=yes
# Esperar reboot
/system identity set name="Router-01-Edge"

# Configuración de interfaces
/ip address add address=192.168.1.1/24 interface=ether2 comment="LAN-PC1"
/ip address add address=10.1.1.1/30 interface=ether5 comment="Link-to-R2"

# Routing estático (CRITICAL: Cada router debe configurar TODAS las rutas)
/ip route add dst-address=192.168.2.0/24 gateway=10.1.1.2 comment="To R2 LAN"
/ip route add dst-address=192.168.3.0/24 gateway=10.1.1.2 comment="To R3 LAN"
/ip route add dst-address=192.168.4.0/24 gateway=10.1.1.2 comment="To R4 LAN"
/ip route add dst-address=192.168.5.0/24 gateway=10.1.1.2 comment="To R5 LAN"
/ip route add dst-address=192.168.6.0/24 gateway=10.1.1.2 comment="To R6 LAN"
/ip route add dst-address=10.1.2.0/30 gateway=10.1.1.2 comment="R2-R3 Link"
/ip route add dst-address=10.1.3.0/30 gateway=10.1.1.2 comment="R3-R4 Link"
/ip route add dst-address=10.1.4.0/30 gateway=10.1.1.2 comment="R4-R5 Link"
/ip route add dst-address=10.1.5.0/30 gateway=10.1.1.2 comment="R5-R6 Link"

# DNS para troubleshooting
/ip dns set servers=8.8.8.8 allow-remote-requests=yes
```

**Router 2 (Grupo 2):**
```bash
/system identity set name="Router-02-Transit"
/ip address add address=10.1.1.2/30 interface=ether1 comment="Link-to-R1"
/ip address add address=192.168.2.1/24 interface=ether2 comment="LAN-PC2"
/ip address add address=10.1.2.1/30 interface=ether5 comment="Link-to-R3"

# Rutas hacia la izquierda (R1)
/ip route add dst-address=192.168.1.0/24 gateway=10.1.1.1 comment="To R1 LAN"

# Rutas hacia la derecha (R3-R6)
/ip route add dst-address=192.168.3.0/24 gateway=10.1.2.2 comment="To R3 LAN"
/ip route add dst-address=192.168.4.0/24 gateway=10.1.2.2 comment="To R4 LAN"
/ip route add dst-address=192.168.5.0/24 gateway=10.1.2.2 comment="To R5 LAN"
/ip route add dst-address=192.168.6.0/24 gateway=10.1.2.2 comment="To R6 LAN"
/ip route add dst-address=10.1.3.0/30 gateway=10.1.2.2 comment="R3-R4 Link"
/ip route add dst-address=10.1.4.0/30 gateway=10.1.2.2 comment="R4-R5 Link"
/ip route add dst-address=10.1.5.0/30 gateway=10.1.2.2 comment="R5-R6 Link"
```

**Router 3 (Grupo 3) - Similar pattern...**
**Router 4 (Grupo 4) - Similar pattern...**
**Router 5 (Grupo 5) - Similar pattern...**
**Router 6 (Grupo 6):**
```bash
/system identity set name="Router-06-Edge"
/ip address add address=10.1.5.2/30 interface=ether1 comment="Link-to-R5"
/ip address add address=192.168.6.1/24 interface=ether2 comment="LAN-PC6"

# Todas las rutas van hacia R5
/ip route add dst-address=192.168.1.0/24 gateway=10.1.5.1 comment="To R1 LAN"
/ip route add dst-address=192.168.2.0/24 gateway=10.1.5.1 comment="To R2 LAN"
/ip route add dst-address=192.168.3.0/24 gateway=10.1.5.1 comment="To R3 LAN"
/ip route add dst-address=192.168.4.0/24 gateway=10.1.5.1 comment="To R4 LAN"
/ip route add dst-address=192.168.5.0/24 gateway=10.1.5.1 comment="To R5 LAN"
/ip route add dst-address=10.1.1.0/30 gateway=10.1.5.1 comment="R1-R2 Link"
/ip route add dst-address=10.1.2.0/30 gateway=10.1.5.1 comment="R2-R3 Link"
/ip route add dst-address=10.1.3.0/30 gateway=10.1.5.1 comment="R3-R4 Link"
/ip route add dst-address=10.1.4.0/30 gateway=10.1.5.1 comment="R4-R5 Link"
```

#### **🧪 Testing y Análisis:**

**Test 1: Connectivity Matrix (15 minutos)**
```bash
# Cada grupo ejecuta desde su router:
/ping 192.168.1.1 count=10 size=64    # PC1
/ping 192.168.2.1 count=10 size=64    # PC2
/ping 192.168.3.1 count=10 size=64    # PC3
/ping 192.168.4.1 count=10 size=64    # PC4
/ping 192.168.5.1 count=10 size=64    # PC5
/ping 192.168.6.1 count=10 size=64    # PC6

# Documentar resultados en matriz:
```

**Connectivity Matrix Template:**
```
         R1    R2    R3    R4    R5    R6
    R1   --   ___   ___   ___   ___   ___
    R2  ___   --    ___   ___   ___   ___
    R3  ___   ___   --    ___   ___   ___
    R4  ___   ___   ___   --    ___   ___
    R5  ___   ___   ___   ___   --    ___
    R6  ___   ___   ___   ___   ___   --

Legend: ✓ = Success, ✗ = Failed, (XXXms) = Average latency
```

**Test 2: Latency Analysis by Hop Count (10 minutos)**
```bash
# Router 1 ejecuta:
/ping 192.168.1.1 count=20 comment="0 hops - local"
/ping 192.168.2.1 count=20 comment="1 hop via R2"
/ping 192.168.3.1 count=20 comment="2 hops via R2-R3"
/ping 192.168.4.1 count=20 comment="3 hops via R2-R3-R4"
/ping 192.168.5.1 count=20 comment="4 hops via R2-R3-R4-R5"
/ping 192.168.6.1 count=20 comment="5 hops via R2-R3-R4-R5-R6"

# Documentar latencia promedio para análisis
```

**Test 3: Traceroute Analysis (10 minutos)**
```bash
# Router 1 traceroute to Router 6:
/tool traceroute 192.168.6.1

# Router 6 traceroute to Router 1:
/tool traceroute 192.168.1.1

# Comparar rutas forward vs return
# ¿Son simétricas? ¿Por qué?
```

**Test 4: Failure Simulation (15 minutos)**
```bash
# Desconectar cable entre R3 y R4
# Cada grupo verifica conectividad:
/ping 192.168.6.1 count=5

# ¿Qué routers pueden aún comunicarse?
# ¿Cuáles quedan aislados?

# Reconectar y verificar recuperación
# ¿Cuánto tiempo toma detectar el enlace?
```

#### **📊 Análisis Requerido:**

**Planilla de Análisis de Routing Estático:**
```
┌─────────────────────────────────────────────────────────┐
│              LABORATORIO                                │
│            Static Routing Analysis                      │
├─────────────────────────────────────────────────────────┤
│ 1. LATENCY vs HOP COUNT                                 │
│    0 hops (local): _______ ms                           │
│    1 hop: _______ ms                                    │
│    2 hops: _______ ms                                   │
│    3 hops: _______ ms                                   │
│    4 hops: _______ ms                                   │
│    5 hops: _______ ms                                   │
│                                                         │
│    Latencia por hop adicional: _______ ms               │
│    ¿Es lineal la relación? ________________             │
│                                                         │
│ 2. ROUTE TABLE ANALYSIS                                 │
│    Total rutas configuradas: _______                    │
│    Rutas activas: _______                               │
│    Rutas por defecto: _______                           │
│                                                         │
│ 3. FAILURE IMPACT                                       │
│    Tiempo sin conectividad: _______ segundos            │
│    Routers afectados: _______                           │
│    Solución automática: Sí/No _______                   │
│                                                         │
│ 4. TROUBLESHOOTING                                      │
│    Problemas encontrados: ___________________           │
│    Comandos útiles: _________________________           │
│    Lecciones aprendidas: ____________________           │
└─────────────────────────────────────────────────────────┘
```

---

### **EXPERIENCIA PRÁCTICA: "DYNAMIC ROUTING PROTOCOL BATTLE"**

#### **🎯 Objetivos:**
- Comparar RIP vs OSPF en tiempo real
- Medir convergencia automática ante fallos
- Analizar overhead de protocolo
- Evaluar escalabilidad de cada solución

#### **🔧 Setup Físico:**
```
Topología en Triángulo + Spokes:

      [RB951-1]
         /    \
        /      \
   [RB951-2]──[RB951-3]
       │        │
   [RB951-4] [RB951-5]
       │
   [RB951-6]
```

#### **📋 Procedimiento por Fases:**

**Fase 1: RIP Implementation (20 minutos)**

**Router 1 (Grupo 1):**
```bash
/system identity set name="RIP-Router-1"

# Configuración básica de interfaces
/ip address add address=192.168.1.1/24 interface=ether2 comment="LAN-1"
/ip address add address=10.0.12.1/30 interface=ether3 comment="Link-to-R2"
/ip address add address=10.0.13.1/30 interface=ether4 comment="Link-to-R3"

# Configuración RIP
/routing rip interface add interface=ether3 send=v2 receive=v2 comment="To-R2"
/routing rip interface add interface=ether4 send=v2 receive=v2 comment="To-R3"

# Redes a anunciar
/routing rip network add network=192.168.1.0/24
/routing rip network add network=10.0.12.0/30
/routing rip network add network=10.0.13.0/30

# Habilitar RIP
/routing rip set distribute-default=never redistribute-connected=yes
```

**Router 2 (Grupo 2):**
```bash
/system identity set name="RIP-Router-2"
/ip address add address=192.168.2.1/24 interface=ether2 comment="LAN-2"
/ip address add address=10.0.12.2/30 interface=ether3 comment="Link-to-R1"
/ip address add address=10.0.23.1/30 interface=ether4 comment="Link-to-R3"
/ip address add address=10.0.24.1/30 interface=ether5 comment="Link-to-R4"

# RIP en todas las interfaces WAN
/routing rip interface add interface=ether3 send=v2 receive=v2
/routing rip interface add interface=ether4 send=v2 receive=v2
/routing rip interface add interface=ether5 send=v2 receive=v2

# Redes
/routing rip network add network=192.168.2.0/24
/routing rip network add network=10.0.12.0/30
/routing rip network add network=10.0.23.0/30
/routing rip network add network=10.0.24.0/30

/routing rip set redistribute-connected=yes
```

**Continuar con Routers 3-6 siguiendo el patrón...**

**Test RIP (10 minutos):**
```bash
# En cada router, verificar tabla RIP:
/routing rip route print detail

# Medir tiempo de convergencia:
# 1. Router 1 desconectar ether3 (link a R2)
/interface ethernet set ether3 disabled=yes

# 2. Cronometrar hasta que Router 6 detecte el cambio
# 3. Router 6 ejecutar:
/ping 192.168.1.1 count=1 interval=5s
# ¿Cuándo deja de funcionar?
# ¿Cuándo vuelve a funcionar por ruta alternativa?

# 4. Reconectar
/interface ethernet set ether3 disabled=no
```

**Fase 2: OSPF Implementation (20 minutos)**

**Router 1 (Configuración OSPF):**
```bash
# Deshabilitar RIP primero
/routing rip set disabled=yes

# Configurar OSPF
/routing ospf instance set default redistribute-connected=as-external-1 router-id=1.1.1.1

# Crear área backbone
/routing ospf area set backbone area-id=0.0.0.0

# Configurar redes en OSPF
/routing ospf network add network=192.168.1.0/24 area=backbone
/routing ospf network add network=10.0.12.0/30 area=backbone
/routing ospf network add network=10.0.13.0/30 area=backbone

# Configurar costos de interfaces
/routing ospf interface add interface=ether3 cost=10 comment="Fast-Link"
/routing ospf interface add interface=ether4 cost=20 comment="Backup-Link"
```

**Repetir para todos los routers con sus respectivas redes...**

**Test OSPF (10 minutos):**
```bash
# Verificar base de datos OSPF
/routing ospf lsa print

# Verificar vecinos OSPF
/routing ospf neighbor print

# Test de convergencia OSPF:
# 1. Router 2 deshabilitar ether3
/interface ethernet set ether3 disabled=no

# 2. Cronometrar convergencia
# 3. Router 6 ping continuo:
/ping 192.168.1.1 count=100 interval=1s

# ¿Cuántos pings se pierden?
# ¿Cuánto tiempo de convergencia?
```

**Fase 3: Protocol Comparison (15 minutos)**

**Performance Benchmark:**
```bash
# Test con RIP activo
/tool bandwidth-test address=192.168.6.1 duration=30s direction=both protocol=tcp

# Monitoreo de CPU durante RIP
/system resource monitor duration=30s

# Cambiar a OSPF
/routing rip set disabled=yes
# (Esperar 2 minutos para stabilidad)

# Test con OSPF activo
/tool bandwidth-test address=192.168.6.1 duration=30s direction=both protocol=tcp

# Monitoreo de CPU durante OSPF
/system resource monitor duration=30s
```

#### **📊 Análisis Comparativo:**

**Planilla de Comparación RIP vs OSPF:**
```
┌─────────────────────────────────────────────────────────┐
│              LABORATORIO                                │
│           RIP vs OSPF Comparison                        │
├─────────────────────────────────────────────────────────┤
│                     RIP        OSPF                     │
│ Convergencia (seg)   ____      ____                     │
│ Pings perdidos       ____      ____                     │
│ CPU overhead (%)     ____      ____                     │
│ Memory usage (KB)    ____      ____                     │
│ Routing table size   ____      ____                     │
│ Config complexity    ____      ____                     │
│ (1=simple, 5=complex)                                   │
│                                                         │
│ FAILURE SCENARIOS:                                      │
│ Single link failure:                                    │
│   RIP recovery: _______ seconds                         │
│   OSPF recovery: _______ seconds                        │
│                                                         │
│ Router failure:                                         │
│   RIP detection: _______ seconds                        │
│   OSPF detection: _______ seconds                       │
│                                                         │
│ SCALABILITY ANALYSIS:                                   │
│ Route advertisements/minute:                             │
│   RIP: _______                                          │
│   OSPF: _______                                         │
│                                                         │
│ TEAM CONCLUSION:                                        │
│ Best protocol for this topology: _____________          │
│ Justification: _________________________               │
│ Scenarios where you'd use RIP: _____________            │
│ Scenarios where you'd use OSPF: ____________            │
└─────────────────────────────────────────────────────────┘
```

---

### ** EXPERIENCIA PRÁCTICA: "VLAN SEGMENTATION ENTERPRISE SIMULATION"**

#### **🎯 Objetivos:**
- Implementar segmentación empresarial realista con VLANs
- Configurar inter-VLAN routing con políticas de seguridad
- Simular diferentes departamentos con acceso diferenciado
- Analizar tráfico broadcast y performance por VLAN

#### **🔧 Setup Físico:**
```
Simulación de Enterprise Network:

[Admin-PC]────ether2[VLAN 10]
[User-PC]─────ether3[VLAN 20]    RB951-Router-Core    ether1[Trunk]────[RB951-Router-Branch]
[Guest-PC]────ether4[VLAN 30]                         
[Server]──────ether5[VLAN 99]

Branch Office:
[Admin-PC]────ether2[VLAN 10]
[User-PC]─────ether3[VLAN 20]    RB951-Router-Branch
[IoT-Device]──ether4[VLAN 40]
```

#### **📋 Procedimiento Detallado:**

**Router Core (Grupos 1-3):**
```bash
/system identity set name="Enterprise-Core"

# 1. Bridge Setup con VLAN Filtering
/interface bridge add name=br-enterprise vlan-filtering=no protocol-mode=rstp

# 2. Agregar puertos físicos
/interface bridge port add bridge=br-enterprise interface=ether2 comment="Admin-Access"
/interface bridge port add bridge=br-enterprise interface=ether3 comment="Users-Access" 
/interface bridge port add bridge=br-enterprise interface=ether4 comment="Guests-Access"
/interface bridge port add bridge=br-enterprise interface=ether5 comment="Servers-Access"
/interface bridge port add bridge=br-enterprise interface=ether1 comment="Trunk-to-Branch"

# 3. Crear VLANs Empresariales
/interface vlan add name=vlan10-admin vlan-id=10 interface=br-enterprise comment="IT-Department"
/interface vlan add name=vlan20-users vlan-id=20 interface=br-enterprise comment="General-Users"
/interface vlan add name=vlan30-guests vlan-id=30 interface=br-enterprise comment="Guest-Network"
/interface vlan add name=vlan40-iot vlan-id=40 interface=br-enterprise comment="IoT-Devices"
/interface vlan add name=vlan99-servers vlan-id=99 interface=br-enterprise comment="Server-Farm"

# 4. VLAN Membership Configuration
/interface bridge vlan add bridge=br-enterprise tagged=br-enterprise,ether1 untagged=ether2 vlan-ids=10
/interface bridge vlan add bridge=br-enterprise tagged=br-enterprise,ether1 untagged=ether3 vlan-ids=20
/interface bridge vlan add bridge=br-enterprise tagged=br-enterprise,ether1 untagged=ether4 vlan-ids=30
/interface bridge vlan add bridge=br-enterprise tagged=br-enterprise,ether1 untagged=none vlan-ids=40
/interface bridge vlan add bridge=br-enterprise tagged=br-enterprise,ether1 untagged=ether5 vlan-ids=99

# 5. PVID Assignment
/interface bridge port set [find interface=ether2] pvid=10
/interface bridge port set [find interface=ether3] pvid=20
/interface bridge port set [find interface=ether4] pvid=30
/interface bridge port set [find interface=ether5] pvid=99

# 6. IP Addressing per Department
/ip address add address=10.10.10.1/24 interface=vlan10-admin comment="Admin-Gateway"
/ip address add address=10.10.20.1/24 interface=vlan20-users comment="Users-Gateway"
/ip address add address=10.10.30.1/24 interface=vlan30-guests comment="Guests-Gateway"
/ip address add address=10.10.40.1/24 interface=vlan40-iot comment="IoT-Gateway"
/ip address add address=10.10.99.1/24 interface=vlan99-servers comment="Servers-Gateway"

# 7. DHCP Pools per VLAN
/ip pool add name=pool-admin ranges=10.10.10.100-10.10.10.199
/ip pool add name=pool-users ranges=10.10.20.100-10.10.20.199
/ip pool add name=pool-guests ranges=10.10.30.100-10.10.30.199
/ip pool add name=pool-iot ranges=10.10.40.100-10.10.40.199

/ip dhcp-server add name=dhcp-admin interface=vlan10-admin address-pool=pool-admin lease-time=8h
/ip dhcp-server add name=dhcp-users interface=vlan20-users address-pool=pool-users lease-time=4h
/ip dhcp-server add name=dhcp-guests interface=vlan30-guests address-pool=pool-guests lease-time=1h
/ip dhcp-server add name=dhcp-iot interface=vlan40-iot address-pool=pool-iot lease-time=24h

/ip dhcp-server network add address=10.10.10.0/24 gateway=10.10.10.1 dns-server=10.10.99.10
/ip dhcp-server network add address=10.10.20.0/24 gateway=10.10.20.1 dns-server=10.10.99.10
/ip dhcp-server network add address=10.10.30.0/24 gateway=10.10.30.1 dns-server=8.8.8.8
/ip dhcp-server network add address=10.10.40.0/24 gateway=10.10.40.1 dns-server=10.10.99.10

# 8. Enterprise Security Policies
/ip firewall filter add chain=forward action=accept src-address=10.10.10.0/24 comment="Admin full access"

/ip firewall filter add chain=forward action=accept src-address=10.10.20.0/24 dst-address=10.10.99.0/24 protocol=tcp dst-port=80,443 comment="Users to web servers"
/ip firewall filter add chain=forward action=accept src-address=10.10.20.0/24 dst-address=10.10.99.0/24 protocol=tcp dst-port=25,587,993,995 comment="Users to mail servers"
/ip firewall filter add chain=forward action=drop src-address=10.10.20.0/24 dst-address=10.10.0.0/16 comment="Block users from other VLANs"

/ip firewall filter add chain=forward action=accept src-address=10.10.30.0/24 dst-address=!10.10.0.0/16 comment="Guests internet only"
/ip firewall filter add chain=forward action=drop src-address=10.10.30.0/24 dst-address=10.10.0.0/16 comment="Block guests from internal"

/ip firewall filter add chain=forward action=drop src-address=10.10.40.0/24 dst-address=!10.10.99.0/24 comment="IoT to servers only"

# 9. Enable VLAN Filtering (CRITICAL: Last step!)
/interface bridge set br-enterprise vlan-filtering=yes
```

**Router Branch (Grupos 4-6):**
```bash
/system identity set name="Enterprise-Branch"

# Similar configuration but as branch office
/interface bridge add name=br-branch vlan-filtering=no

# Trunk connection to core
/interface bridge port add bridge=br-branch interface=ether1 comment="Trunk-to-Core"
/interface bridge port add bridge=br-branch interface=ether2 comment="Branch-Admin"
/interface bridge port add bridge=br-branch interface=ether3 comment="Branch-Users"
/interface bridge port add bridge=br-branch interface=ether4 comment="Branch-IoT"

# Same VLANs but branch addressing
/interface vlan add name=vlan10-branch vlan-id=10 interface=br-branch
/interface vlan add name=vlan20-branch vlan-id=20 interface=br-branch
/interface vlan add name=vlan40-branch vlan-id=40 interface=br-branch

/ip address add address=10.20.10.1/24 interface=vlan10-branch comment="Branch-Admin"
/ip address add address=10.20.20.1/24 interface=vlan20-branch comment="Branch-Users"  
/ip address add address=10.20.40.1/24 interface=vlan40-branch comment="Branch-IoT"

# Branch VLAN membership
/interface bridge vlan add bridge=br-branch tagged=ether1,br-branch untagged=ether2 vlan-ids=10
/interface bridge vlan add bridge=br-branch tagged=ether1,br-branch untagged=ether3 vlan-ids=20
/interface bridge vlan add bridge=br-branch tagged=ether1,br-branch untagged=ether4 vlan-ids=40

/interface bridge port set [find interface=ether2] pvid=10
/interface bridge port set [find interface=ether3] pvid=20
/interface bridge port set [find interface=ether4] pvid=40

/interface bridge set br-branch vlan-filtering=yes
```

#### **🧪 Testing y Análisis Enterprise:**

**Test 1: Department Isolation Verification (15 minutos)**
```bash
# From Admin VLAN (should work):
ping 10.10.20.1    # Users gateway
ping 10.10.99.1    # Servers gateway
ping 10.10.30.1    # Guests gateway
ping 10.20.10.1    # Branch admin

# From Users VLAN (limited access):
ping 10.10.99.10   # Server (should work for web)
ping 10.10.10.100  # Admin PC (should fail)
ping 10.10.30.100  # Guest PC (should fail)

# From Guests VLAN (internet only):
ping 8.8.8.8       # Internet (should work)
ping 10.10.20.100  # User PC (should fail)
ping 10.10.99.10   # Server (should fail)

# Document results:
```

**Test 2: Broadcast Domain Analysis (10 minutos)**
```bash
# Enable broadcast monitoring
/tool sniffer set filter-stream=yes filter-mac-protocol=ip 
/tool sniffer start interface=ether2 duration=60

# Generate broadcast traffic from Admin PC
# (ping broadcast address, DHCP renewal, etc.)

/tool sniffer stop
/tool sniffer packet print

# Count broadcast packets per VLAN
# Verify isolation is working
```

**Test 3: VLAN Performance Impact (15 minutos)**
```bash
# Baseline - single VLAN performance
/tool bandwidth-test address=10.10.20.100 duration=30s direction=both

# Cross-VLAN routing performance  
/tool bandwidth-test address=10.10.99.10 duration=30s direction=both

# Inter-site VLAN performance (Core to Branch)
/tool bandwidth-test address=10.20.20.100 duration=30s direction=both

# Monitor CPU during tests
/system resource monitor duration=30s

# Document performance differences
```

**Test 4: Security Policy Validation (10 minutos)**
```bash
# Attempt forbidden connections and document results:

# From Users VLAN, try to access Admin:
/tool telnet 10.10.10.100 port=22
# Result: __________________

# From Guests, try to access internal server:
/tool telnet 10.10.99.10 port=80  
# Result: __________________

# From IoT VLAN, try to access Users:
/tool telnet 10.10.20.100 port=445
# Result: __________________

# Verify firewall logs:
/log print where topics~"firewall"
```

#### **📊 Enterprise Analysis Report:**

**Planilla de Análisis Enterprise VLAN:**
```
┌─────────────────────────────────────────────────────────┐
│              LABORATORIO                                │
│           Enterprise VLAN Implementation                │
├─────────────────────────────────────────────────────────┤
│ 1. VLAN SEGMENTATION EFFECTIVENESS                      │
│    VLANs configured: _______                            │
│    Broadcast domains isolated: Yes/No _______           │
│    Cross-VLAN leakage detected: Yes/No _______          │
│                                                         │
│ 2. SECURITY POLICY ENFORCEMENT                          │
│    Admin → All VLANs: ✓/✗ _______                      │
│    Users → Servers only: ✓/✗ _______                   │
│    Users → Admin blocked: ✓/✗ _______                  │
│    Guests → Internet only: ✓/✗ _______                 │
│    Guests → Internal blocked: ✓/✗ _______              │
│    IoT → Servers only: ✓/✗ _______                     │
│                                                         │
│ 3. PERFORMANCE IMPACT                                   │
│    Baseline throughput: _______ Mbps                    │
│    Inter-VLAN throughput: _______ Mbps                  │
│    Inter-site throughput: _______ Mbps                  │
│    CPU overhead with VLANs: _______ %                   │
│                                                         │
│ 4. OPERATIONAL COMPLEXITY                               │
│    Configuration time: _______ minutes                  │
│    Troubleshooting difficulty (1-10): _______           │
│    Most challenging aspect: ___________________         │
│                                                         │
│ 5. BUSINESS VALUE ASSESSMENT                            │
│    Security improvement: Low/Med/High _______           │
│    Network manageability: Worse/Same/Better _______     │
│    Scalability for growth: Poor/Good/Excellent _______  │
│                                                         │
│ 6. RECOMMENDATIONS                                      │
│    VLAN design improvements: ____________________       │
│    Additional security measures: _________________      │
│    Performance optimizations: ____________________     │
└─────────────────────────────────────────────────────────┘
```

---

### **EXPERIENCIAS ADICIONALES PARA CLASES RESTANTES**

**CLASE - "INTER-VLAN ROUTING OPTIMIZATION"**
- Router-on-a-stick vs L3 switching performance
- VLAN pruning y optimization
- QoS implementation per VLAN

**CLASE - "ADVANCED TUNNELING LAB"**  
- GRE tunnels between sites
- Basic VPN setup
- Overlay network concepts

**CLASE  - "SNMP MONITORING DEPLOYMENT"**
- Full SNMP implementation 
- Custom OID monitoring
- Centralized management setup

**CLASE  - "NETWORK PERFORMANCE BASELINE"**
- Establish performance baselines
- Create monitoring dashboards
- Alert threshold configuration

¿Te gustaría que desarrolle las experiencias prácticas para las clases restantes (7-32) con el mismo nivel de detalle?

### **Experiencia 2: VLAN Implementation (Grupal)**

#### **Objetivos:**
- Implementar segmentación VLAN
- Configurar inter-VLAN routing
- Establecer políticas de seguridad

#### **Topología:**
```
[PC1-Admin] ──── ether2 (VLAN 10)
                      │
[PC2-Users] ──── ether3 (VLAN 20) ──── RB951-2HnD ──── ether5 (Trunk)
                      │
[PC3-Guests] ─── ether4 (VLAN 30)
```

#### **Procedimiento Completo:**
```bash
# 1. Preparación
/interface bridge remove [find]
/interface vlan remove [find]

# 2. Configuración base
/interface bridge add name=br-main vlan-filtering=no
/interface bridge port add bridge=br-main interface=ether2 comment="Admin"
/interface bridge port add bridge=br-main interface=ether3 comment="Users"
/interface bridge port add bridge=br-main interface=ether4 comment="Guests"
/interface bridge port add bridge=br-main interface=ether5 comment="Trunk"

# 3. Interfaces VLAN
/interface vlan add name=vlan10 vlan-id=10 interface=br-main comment="Admin"
/interface vlan add name=vlan20 vlan-id=20 interface=br-main comment="Users"
/interface vlan add name=vlan30 vlan-id=30 interface=br-main comment="Guests"

# 4. VLAN Membership
/interface bridge vlan add bridge=br-main tagged=br-main,ether5 untagged=ether2 vlan-ids=10
/interface bridge vlan add bridge=br-main tagged=br-main,ether5 untagged=ether3 vlan-ids=20
/interface bridge vlan add bridge=br-main tagged=br-main,ether5 untagged=ether4 vlan-ids=30

# 5. PVID Configuration
/interface bridge port set [find interface=ether2] pvid=10
/interface bridge port set [find interface=ether3] pvid=20
/interface bridge port set [find interface=ether4] pvid=30

# 6. IP Addressing
/ip address add address=192.168.10.1/24 interface=vlan10 comment="Admin Gateway"
/ip address add address=192.168.20.1/24 interface=vlan20 comment="Users Gateway"
/ip address add address=192.168.30.1/24 interface=vlan30 comment="Guests Gateway"

# 7. Enable VLAN Filtering
/interface bridge set br-main vlan-filtering=yes
```

#### **Testing Protocol:**
1. **Conectar PCs** a cada puerto access
2. **Configurar IPs estáticas** en cada PC
3. **Verificar conectividad intra-VLAN**
4. **Verificar aislamiento inter-VLAN**
5. **Configurar firewall** para políticas específicas

---

## 🏠 **PRÁCTICA EN CASA CON GNS3**

### **Setup GNS3 para RouterOS**

#### **Requisitos del Sistema:**
- **RAM:** 8GB mínimo (16GB recomendado)
- **CPU:** Soporte virtualización (Intel VT-x/AMD-V)
- **Espacio:** 20GB libres
- **SO:** Windows 10/11, macOS, Linux

#### **Instalación Paso a Paso:**

**1. Descargar GNS3:**
- Ir a https://gns3.com/software/download
- Descargar GNS3 GUI + VM para tu SO
- Instalar siguiendo wizard

**2. Configurar RouterOS CHR:**
```bash
# Descargar Cloud Hosted Router (CHR) de MikroTik
# URL: https://mikrotik.com/download
# Archivo: chr-6.49.10.vdi (VirtualBox format)
```

**3. Importar en GNS3:**
- Open GNS3 → Edit → Preferences → Dynamips → IOS routers
- New → Browse CHR image → Configure RAM (256MB)
- Advanced → Enable KVM if available

### **Laboratorio Virtual 1: Topología Básica**

#### **Escenario:**
```
[PC1] ──── [RouterOS-1] ──── [RouterOS-2] ──── [PC2]
```

#### **Configuración:**

**RouterOS-1:**
```bash
/ip address add address=192.168.1.1/24 interface=ether1
/ip address add address=10.0.0.1/30 interface=ether2
/ip route add dst-address=192.168.2.0/24 gateway=10.0.0.2
```

**RouterOS-2:**
```bash
/ip address add address=10.0.0.2/30 interface=ether1
/ip address add address=192.168.2.1/24 interface=ether2
/ip route add dst-address=192.168.1.0/24 gateway=10.0.0.1
```

### **Laboratorio Virtual 2: VLANs Multi-Switch**

#### **Escenario:**
```
[PC-Admin] ── [Switch1] ──── [Switch2] ── [PC-Users]
                 │    Trunk    │
             [PC-Local]    [PC-Remote]
```

#### **Configuración Switch1:**
```bash
/interface bridge add name=br-main vlan-filtering=yes
/interface bridge port add bridge=br-main interface=ether1 comment="PC-Admin"
/interface bridge port add bridge=br-main interface=ether2 comment="PC-Local"
/interface bridge port add bridge=br-main interface=ether3 comment="Trunk"

/interface vlan add name=vlan10 vlan-id=10 interface=br-main
/interface vlan add name=vlan20 vlan-id=20 interface=br-main

/interface bridge vlan add bridge=br-main tagged=ether3,br-main untagged=ether1 vlan-ids=10
/interface bridge vlan add bridge=br-main tagged=ether3,br-main untagged=ether2 vlan-ids=20

/interface bridge port set [find interface=ether1] pvid=10
/interface bridge port set [find interface=ether2] pvid=20
```
---

