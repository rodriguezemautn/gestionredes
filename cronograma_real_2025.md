# CRONOGRAMA REAL 2025
## GESTIÓN OPERATIVA Y SEGURIDAD EN REDES
**Ingeniería en Sistemas de Información - 5º Nivel**

**Modalidad:** Martes 18:00-20:15 hs | Sábados 9:00-11:15 hs  
**Duración:** 12 de Agosto - 29 de Noviembre 2025  
**Total:** 32 clases × 2.25 hs = 72 horas reloj

---

## 📅 AGOSTO 2025

### **CLASE 1 - Martes 12/08 (18:00-20:15)**
**🎯 PRESENTACIÓN DE LA MATERIA + REPASO REDES**

#### **Contenido:**
- **Presentación docentes y metodología** (30 min)
- **Objetivos y resultados de aprendizaje** (20 min)
- **Cronograma y evaluaciones** (20 min)
- **Repaso conceptos fundamentales de redes:** (45 min)
  * Modelo OSI/TCP-IP
  * Subnetting y VLSM 
  * Routing básico
  * Switching fundamentals
- **Presentación equipamiento:** Router MikroTik RB951-2HnD (20 min)

#### **Actividades:**
- Quiz diagnóstico conocimientos previos
- Formación de grupos de trabajo (6 grupos)
- Asignación inicial de routers
- Test conectividad básica equipos

---

### **CLASE 2 - Sábado 16/08 (9:00-11:15)**
**📡 UNIDAD 1: Administración de Routers**

#### **Temas:**
1. **Introducción a Routers Avanzados**
   - Arquitectura del RB951-2HnD
   - RouterOS overview y licencias
   - Métodos de acceso (Winbox, WebFig, SSH, Console)

2. **Configuración Inicial**
   - Factory reset y first configuration
   - IP addressing y interface naming
   - Basic routing table

#### **Experiencias con RB951-2HnD:**
**Por Grupo (6 grupos, 1 router c/u):**
- Reconocimiento físico completo del hardware
- Primera configuración via Winbox
- Setup de IP management y conectividad básica

**Entre Grupos:**
- "Router Setup Race" - configuración más rápida
- Comparación de métodos de acceso

---

### **CLASE 3 - Martes 19/08 (18:00-20:15)**
**🛣️ PROTOCOLOS DE ENRUTAMIENTO ESTÁTICO**

#### **Temas:**
1. **Rutas Estáticas en RouterOS**
   - Sintaxis y configuración
   - Default routes y route preferences
   - Route scoping y distance

2. **Troubleshooting Routing**
   - Herramientas de diagnóstico
   - Traceroute y ping avanzado
   - Route monitoring

#### **Experiencias con RB951-2HnD:**
**Por Grupo:**
- Configuración de rutas estáticas complejas
- Setup de múltiples gateways
- Testing de redundancia de rutas

**Entre Grupos:**
- Topología lineal: Router1→Router2→...→Router6
- Ping end-to-end competition
- Troubleshooting de conectividad entre grupos

---

### **CLASE 4 - Sábado 23/08 (9:00-11:15)**
**🔄 PROTOCOLOS DE ENRUTAMIENTO DINÁMICO**

#### **Temas:**
1. **RIP en RouterOS**
   - Configuración RIPv2
   - Métricas y convergencia
   - RIP authentication

2. **OSPF Fundamentals**
   - Single-area OSPF
   - LSA types básicos
   - Neighbor relationships

#### **Experiencias con RB951-2HnD:**
**Por Grupo (reorganización en 3 duplas):**
- Dupla A: Router1-Router2 con RIP
- Dupla B: Router3-Router4 con OSPF
- Dupla C: Router5-Router6 con Static

**Entre Grupos:**
- "Protocol Battle" - comparar performance
- Convergence timing tests
- Merge de topologías con protocolo único

---

### **CLASE 5 - Martes 26/08 (18:00-20:15)**
**🔧 GESTIÓN AVANZADA DE ROUTERS**

#### **Temas:**
1. **RouterOS Scripting**
   - Sintaxis básica
   - Variables y loops
   - Automation scripts

2. **Monitoring y Management**
   - SNMP configuration
   - Netwatch setup
   - Backup y restore procedures

#### **Experiencias con RB951-2HnD:**
**Por Grupo:**
- Creación de scripts de automatización
- Setup SNMP y monitoring básico
- Configuración de alertas automáticas

**Entre Grupos:**
- Script sharing y documentation
- Best practices workshop
- Automated backup competition

---

### **CLASE 6 - Sábado 30/08 (9:00-11:15)**
**🌐 UNIDAD 2: Redes Virtuales - VLAN Fundamentals**

#### **Temas:**
1. **VLANs en RouterOS**
   - VLAN interfaces creation
   - 802.1Q tagging
   - Bridge VLAN filtering

2. **Switch Configuration**
   - Master-port configuration
   - VLAN membership
   - Trunk vs Access ports

#### **Experiencias con RB951-2HnD:**
**Por Grupo (vuelta a 6 grupos individuales):**
- Configurar 3 VLANs por router (Admin, Users, Guests)
- Setup trunk en ether5 para interconexión
- Access ports en ether2-4

**Entre Grupos:**
- VLAN spanning entre routers
- "VLAN Olympics" - segmentación más creativa
- Broadcast domain testing

---

## 📅 SEPTIEMBRE 2025

### **CLASE 7 - Martes 02/09 (18:00-20:15)**
**🔗 INTER-VLAN ROUTING**

#### **Temas:**
1. **Router-on-a-Stick**
   - Subinterfaces configuration
   - VLAN routing performance
   - Security considerations

2. **Layer 3 Switching**
   - SVI (Switch Virtual Interfaces)
   - Routing between VLANs
   - VLAN pruning

#### **Experiencias con RB951-2HnD:**
**Por Grupo:**
- Configurar inter-VLAN routing
- Implementar VLAN security policies
- Performance testing entre VLANs

**Entre Grupos:**
- Complex VLAN topologies
- Security policy enforcement testing
- Troubleshooting VLAN communication issues

---

### **CLASE 8 - Sábado 06/09 (9:00-11:15)**
**☁️ VIRTUALIZACIÓN AVANZADA**

#### **Temas:**
1. **Conceptos SDN en RouterOS**
   - OpenFlow support (limitations)
   - CAPsMAN for centralized management
   - Cloud integration concepts

2. **Tunneling Protocols**
   - GRE tunnels
   - IPSec fundamentals
   - L2TP concepts

#### **Experiencias con RB951-2HnD:**
**Por Grupo:**
- Setup GRE tunnels entre routers
- Basic VPN configuration
- Centralized management setup

**Entre Grupos:**
- Overlay network simulation
- Site-to-site VPN lab
- Performance impact analysis

---

### **CLASE 9 - Martes 09/09 (18:00-20:15)**
**📊 UNIDAD 3: Monitoreo - SNMP y Protocolos**

#### **Temas:**
1. **SNMP en RouterOS**
   - SNMPv2c vs SNMPv3
   - Community configuration
   - MIB exploration

2. **Traffic Monitoring**
   - Interface statistics
   - Bandwidth monitoring
   - Connection tracking

#### **Experiencias con RB951-2HnD:**
**Por Grupo:**
- Configurar SNMP en routers
- Setup monitoring PC con Zabbix/Nagios
- Custom monitoring scripts

**Entre Grupos:**
- Central monitoring setup
- "NOC Competition" - best dashboard
- SNMP walk y MIB analysis

---

### **CLASE 10 - Sábado 13/09 (9:00-11:15)**
**📈 HERRAMIENTAS DE MONITOREO**

#### **Temas:**
1. **Zabbix Integration**
   - Agent vs SNMP monitoring
   - Template creation
   - Alert configuration

2. **Log Management**
   - Syslog configuration
   - Log rotation y retention
   - Centralized logging

#### **Experiencias con RB951-2HnD:**
**Por Grupo:**
- Deploy Zabbix monitoring completo
- Configurar syslog centralizado
- Create custom dashboards

**Entre Grupos:**
- Monitoring infrastructure setup
- Alert tuning workshop
- Performance baseline establishment

---

### **CLASE 11 - Martes 16/09 (18:00-20:15)**
**⚖️ UNIDAD 4: Balanceo de Carga - Conceptos**

#### **Temas:**
1. **Load Balancing en RouterOS**
   - Multi-WAN setup
   - Policy routing
   - Connection marking

2. **High Availability Basics**
   - VRRP configuration
   - Failover mechanisms
   - Health checking

#### **Experiencias con RB951-2HnD:**
**Por Grupo (3 grupos con 2 routers c/u):**
- Basic load balancing entre interfaces
- Setup web server simulation en RouterOS
- Health check configuration

**Entre Grupos:**
- "Load Balancer Challenge"
- Algorithm comparison testing
- Failover simulation y timing

---

### **CLASE 12 - Sábado 20/09 (9:00-11:15)**
**🔄 ALTA DISPONIBILIDAD**

#### **Temas:**
1. **VRRP Implementation**
   - Master/Backup configuration
   - Priority tuning
   - Preemption settings

2. **Advanced Failover**
   - Script-based failover
   - Service monitoring
   - Geographic redundancy concepts

#### **Experiencias con RB951-2HnD:**
**Por Grupo:**
- VRRP cluster configuration
- Automated failover testing
- Service-level health monitoring

**Entre Grupos:**
- "HA Olympics" - fastest failover
- Chaos engineering simulation
- Multi-site redundancy planning

---

### **CLASE 13 - Martes 23/09 (18:00-20:15)**
**📝 PRIMER PARCIAL**
**Evaluación:** RA1 (Routers) + RA2 (VLANs) + RA3 (Monitoring)

#### **Formato:**
- **Teórico:** 45 minutos - conceptos fundamentales
- **Práctico:** 90 minutos - configuración en routers
- **Evaluación grupal:** troubleshooting colaborativo

#### **Temario:**
- Configuración completa de RouterOS
- VLAN implementation y troubleshooting  
- SNMP monitoring setup
- Protocol selection y justification

---

### **CLASE 14 - Sábado 27/09 (9:00-11:15)**
**🔍 REVISIÓN PRIMER PARCIAL**

#### **Actividades:**
- Revisión detallada de examen
- Refuerzo de conceptos débiles
- Laboratorio de recuperación
- Q&A session personalizada

---

### **CLASE 15 - Martes 30/09 (18:00-20:15)**
**📝 PRIMER PARCIAL - 2DA FECHA**

---

## 📅 OCTUBRE 2025

### **CLASE 16 - Sábado 04/10 (9:00-11:15)**
**🔍 REVISIÓN PRIMER PARCIAL 2DA FECHA**

---

### **CLASE 17 - Martes 07/10 (18:00-20:15)**
**🔒 UNIDAD 5: Seguridad - Firewall y ACLs**

#### **Temas:**
1. **RouterOS Firewall**
   - Filter rules (input, forward, output)
   - NAT configuration
   - Mangle rules basics

2. **Access Control**
   - Address lists
   - Port knocking
   - Connection limiting

#### **Experiencias con RB951-2HnD:**
**Por Grupo:**
- Comprehensive firewall setup
- NAT y port forwarding
- Security policy implementation

**Entre Grupos:**
- "Security Audit" - peer review
- Attack simulation y defense
- Compliance verification

---

### **CLASE 18 - Sábado 11/10 (9:00-11:15)**
**🔐 AUTENTICACIÓN Y AUTORIZACIÓN**

#### **Temas:**
1. **User Management**
   - Local users y groups
   - SSH key authentication
   - Certificate management

2. **RADIUS Integration**
   - FreeRADIUS setup
   - User authentication flow
   - Accounting y session management

#### **Experiencias con RB951-2HnD:**
**Por Grupo:**
- RADIUS server deployment
- WiFi WPA2-Enterprise setup
- User session tracking

**Entre Grupos:**
- "Corporate WiFi" simulation
- Multi-domain authentication
- Session management testing

---

### **CLASE 19 - Martes 14/10 (18:00-20:15)**
**🏢 ACTIVE DIRECTORY INTEGRATION**

#### **Temas:**
1. **Enterprise Authentication**
   - LDAP integration concepts
   - Windows domain authentication
   - Group policy implications

2. **Network Access Control**
   - 802.1X basics
   - Dynamic VLAN assignment
   - Guest network management

#### **Experiencias con RB951-2HnD:**
**Por Grupo (3 grupos con 2 routers + Windows Server):**
- AD domain setup simulation
- LDAP authentication testing
- Policy-based access control

**Entre Grupos:**
- "Enterprise Network" simulation
- Cross-domain trust scenarios
- Centralized management workshop

---

### **CLASE 20 - Sábado 18/10 (9:00-11:15)**
**📝 PRIMER PARCIAL - 3RA FECHA**

---

### **CLASE 21 - Martes 21/10 (18:00-20:15)**
**🔍 REVISIÓN PRIMER PARCIAL 3RA FECHA**

---

### **CLASE 22 - Sábado 25/10 (9:00-11:15)**
**🛡️ UNIDAD 6: Prevención de Ataques**

#### **Temas:**
1. **Router Hardening**
   - Service minimization
   - Strong authentication
   - Security best practices

2. **Intrusion Prevention**
   - Basic IPS using firewall
   - Rate limiting
   - Blacklist management

#### **Experiencias con RB951-2HnD:**
**Por Grupo:**
- Complete security hardening
- IPS rule implementation
- Attack surface reduction

**Entre Grupos:**
- "Red Team vs Blue Team"
- Security competition
- Penetration testing basics

---

### **CLASE 23 - Martes 28/10 (18:00-20:15)**
**🔍 DETECCIÓN DE ATAQUES**

#### **Temas:**
1. **Intrusion Detection**
   - Log analysis techniques
   - Anomaly detection
   - Signature-based detection

2. **Traffic Analysis**
   - Packet capture analysis
   - Flow-based monitoring
   - Behavioral baselines

#### **Experiencias con RB951-2HnD:**
**Por Grupo:**
- IDS deployment (Suricata/Snort on PC)
- Traffic mirroring setup
- Custom detection rules

**Entre Grupos:**
- "Attack Detection Race"
- False positive tuning
- Correlation analysis workshop

---

## 📅 NOVIEMBRE 2025

### **CLASE 24 - Sábado 01/11 (9:00-11:15)**
**📊 SIEM Y CORRELACIÓN**

#### **Temas:**
1. **Security Information Management**
   - Log aggregation
   - Event correlation
   - Incident prioritization

2. **ELK Stack Basics**
   - Elasticsearch fundamentals
   - Logstash configuration
   - Kibana dashboards

#### **Experiencias con RB951-2HnD:**
**Por Grupo:**
- ELK deployment para logs de routers
- Custom security dashboards
- Alert correlation rules

**Entre Grupos:**
- "SOC Simulation"
- Incident investigation workshop
- Threat hunting exercise

---

### **CLASE 25 - Martes 04/11 (18:00-20:15)**
**🚨 RESPUESTA A INCIDENTES**

#### **Temas:**
1. **Incident Response Process**
   - Detection y triage
   - Containment strategies
   - Evidence preservation

2. **Recovery Planning**
   - Service restoration
   - Business continuity
   - Lessons learned process

#### **Experiencias con RB951-2HnD:**
**Por Grupo:**
- Incident response simulation
- Forensics data collection
- Recovery procedures testing

**Entre Grupos:**
- Tabletop exercise
- Cross-team incident coordination
- Communication drill

---

### **CLASE 26 - Sábado 08/11 (9:00-11:15)**
**📝 SEGUNDO PARCIAL**
**Evaluación:** RA4 (Load Balancing) + RA5 (Security) + RA6 (Incident Response)

#### **Formato:**
- **Teórico:** 45 minutos - security frameworks y procedures
- **Práctico:** 90 minutos - comprehensive security setup
- **Caso de estudio:** incident response scenario

---

### **CLASE 27 - Martes 11/11 (18:00-20:15)**
**🔍 REVISIÓN SEGUNDO PARCIAL**

---

### **CLASE 28 - Sábado 15/11 (9:00-11:15)**
**📝 SEGUNDO PARCIAL - 2DA FECHA**

---

### **CLASE 29 - Martes 18/11 (18:00-20:15)**
**🔍 REVISIÓN SEGUNDO PARCIAL 2DA FECHA**

---

### **CLASE 30 - Sábado 22/11 (9:00-11:15)**
**📝 SEGUNDO PARCIAL - 3RA FECHA**

---

### **CLASE 31 - Martes 25/11 (18:00-20:15)**
**🎯 TRABAJO INTEGRADOR - PRESENTACIONES**

#### **Proyectos Finales:**
- **Grupo 1-2:** Diseño completo de red empresarial
- **Grupo 3-4:** Security Operations Center (SOC)
- **Grupo 5-6:** Disaster Recovery Plan
- **Evaluación:** Presentación + demo en vivo + documentación

---

### **CLASE 32 - Sábado 29/11 (9:00-11:15)**
**🏁 CIERRE DE MATERIA**

#### **Actividades:**
- **Evaluaciones finales pendientes**
- **Feedback del curso**
- **Certificados de participación**
- **Networking y cierre social**

---

## 📊 RESUMEN 

### **Distribución Temporal:**
- **Agosto:** 5 clases - Introducción + Unidad 1 (Routers)
- **Septiembre:** 8 clases - Unidad 2 (VLANs) + Unidad 3 (Monitoring) + 1er Parcial
- **Octubre:** 8 clases - Unidad 4 (Load Balancing) + Unidad 5 (Security) + Recuperatorios
- **Noviembre:** 11 clases - Unidad 6 (Security Ops) + 2do Parcial + Cierre

### **Instancias de Evaluación:**
- **1er Parcial:** 23/09 (+ recuperatorios 30/09 y 20/10)
- **2do Parcial:** 08/11 (+ recuperatorios 15/11 y 22/11)  
- **Trabajo Integrador:** 25/11
- **Evaluación continua:** Laboratorios semanales

### **Metodología:**
- **2.25 hs por clase** optimizado para teoría + práctica
- **6 routers RB951-2HnD** con rotación entre grupos
- **Experiencias escaladas** de individual a colaborativo
- **Assessment continuo** con feedback inmediato

### **Recursos Necesarios:**
- 6 routers MikroTik RB951-2HnD
- 6-8 PCs para monitoring y servers
- Switch managed central
- Cables de red y accesorios
- Proyector y WiFi institucional

¿Te parece bien esta distribución temporal? ¿Hay alguna fecha específica que necesite ajustarse por feriados o eventos institucionales?