
## 📝 **APUNTES COMPLETOS PARA ESTUDIANTE**

### **Apuntes Unidad 1: Administración de Routers**

#### **Conceptos Clave para Recordar**

**1. Router vs Switch vs Hub**
```
┌─────────────┬─────────────┬─────────────┬─────────────┐
│ Aspecto     │    Hub      │   Switch    │   Router    │
├─────────────┼─────────────┼─────────────┼─────────────┤
│ Capa OSI    │ Física (1)  │ Enlace (2)  │ Red (3)     │
│ Dominio     │ Colisión    │ Colisión    │ Broadcast   │
│ Inteligencia│ Ninguna     │ MAC Table   │ Routing     │
│ Seguridad   │ Baja        │ Media       │ Alta        │
└─────────────┴─────────────┴─────────────┴─────────────┘
```

**2. Tabla de Rutas - Componentes**
- **Destination Network:** Red de destino
- **Subnet Mask:** Máscara de subred
- **Next Hop:** Próximo salto (IP del siguiente router)
- **Interface:** Interfaz de salida
- **Metric:** Valor para seleccionar mejor ruta
- **Administrative Distance:** Confiabilidad de la fuente

**3. Comandos RouterOS Esenciales**
```bash
# Ver tabla de rutas
/ip route print

# Ver interfaces
/interface print

# Ver direcciones IP
/ip address print

# Monitoring en tiempo real
/interface monitor-traffic ether1

# Ping con source específico
/ping 8.8.8.8 src-address=192.168.1.1
```

**4. Troubleshooting Routing**
```bash
# 1. Verificar conectividad local
/ping 192.168.1.1

# 2. Verificar gateway
/ping 10.0.0.1

# 3. Traceroute para ver ruta
/tool traceroute 8.8.8.8

# 4. Verificar DNS
/ping google.com

# 5. Ver logs de sistema
/log print where topics~"error"
```

### **Apuntes Unidad 2: Configuración de Redes Virtuales**

#### **Conceptos Clave para Recordar**

**1. VLAN Benefits Checklist**
- ✅ **Segmentación lógica** sin cambios físicos
- ✅ **Reducción de tráfico broadcast** (performance)
- ✅ **Aislamiento de seguridad** entre departamentos
- ✅ **Flexibilidad** para cambios organizacionales
- ✅ **Escalabilidad** hasta 4094 VLANs

**2. VLAN Configuration Checklist**
```bash
# ✅ 1. Crear bridge con VLAN filtering disabled inicialmente
/interface bridge add name=br-main vlan-filtering=no

# ✅ 2. Agregar puertos al bridge
/interface bridge port add bridge=br-main interface=ether2

# ✅ 3. Crear interfaces VLAN
/interface vlan add name=vlan10 vlan-id=10 interface=br-main

# ✅ 4. Configurar VLAN membership
/interface bridge vlan add bridge=br-main tagged=br-main untagged=ether2 vlan-ids=10

# ✅ 5. Configurar PVID
/interface bridge port set [find interface=ether2] pvid=10

# ✅ 6. Habilitar VLAN filtering (¡ÚLTIMO PASO!)
/interface bridge set br-main vlan-filtering=yes
```

**3. VLAN Troubleshooting Guide**
```bash
# Problema: No hay comunicación entre VLANs
# Solución: Verificar routing entre interfaces VLAN
/ip route print where dst-address~"192.168"

# Problema: Trunk no funciona
# Solución: Verificar tagged ports
/interface bridge vlan print where vlan-ids=10

# Problema: Access port no asigna VLAN
# Solución: Verificar PVID
/interface bridge port print detail where interface=ether2

# Problema: Performance degradado
# Solución: Verificar VLAN filtering habilitado
/interface bridge print detail where name=br-main
```

---
