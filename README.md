# Proyecto InnovateTech

---
- Para ver el documento con las imagenes hace falta importar el archivo en un visualizador de archivos.
## Índice

1. [Propuesta del CPD](#propuesta-del-cpd)
   - [Ubicación física](#ubicación-física)
     - [Situación física de la sala del edificio](#situación-física-de-la-sala-del-edificio)
     - [Sistema de climatización](#sistema-de-climatización)
     - [Medidas para dificultar la identificación de la sala](#medidas-para-dificultar-la-identificación-de-la-sala)
     - [Distribución y gestión del cableado](#distribución-y-gestión-del-cableado)
     - [Suelo técnico y techo técnico](#suelo-técnico-y-techo-técnico)
     - [Plano](#plano)
     - [Estructuración de los racks](#estructuración-de-los-racks)
   - [Infraestructura IT](#infraestructura-it)
     - [Servidores](#servidores)
     - [Patch panels](#patch-panels)
     - [Switches](#switches)
     - [Router y Access Point](#router-y-access-point)
     - [Diagramas y distribución](#diagramas-y-distribución)
   - [Infraestructura eléctrica](#infraestructura-eléctrica)
     - [Sistemas de alimentación redundante](#sistemas-de-alimentación-redundante)
     - [SAIs](#sais)
     - [Distribución eléctrica](#distribución-eléctrica)
   - [Seguridad física y lógica](#seguridad-física-y-lógica)
     - [Seguridad física](#seguridad-física)
       - [Control de acceso](#control-de-acceso)
       - [Videovigilancia](#videovigilancia)
       - [Sensor de movimiento](#sensor-de-movimiento)
       - [Sensor de apertura de puerta](#sensor-de-apertura-de-puerta)
       - [Sensor de fuga de agua](#sensor-de-fuga-de-agua)
       - [Control de temperatura y humedad](#control-de-temperatura-y-humedad)
       - [Detección y extinción de incendios](#detección-y-extinción-de-incendios)
       - [Climatización](#climatización)
       - [Vías de evacuación](#vías-de-evacuación)
       - [Plano de seguridad física](#plano-de-seguridad-física)
     - [Seguridad lógica](#seguridad-lógica)
       - [Restricción de acceso por autorización](#restricción-de-acceso-por-autorización)
       - [Firewalls y segmentación de red](#firewalls-y-segmentación-de-red)
       - [AWS Security Groups](#aws-security-groups)
       - [Monitorización](#monitorización)
       - [Copias de seguridad / Backups](#copias-de-seguridad--backups)
       - [RAIDs](#raids)
   - [Prevención de riesgos laborales](#prevención-de-riesgos-laborales)
     - [Medidas aplicadas en materia de prevención de RRLL en el CPD](#medidas-aplicadas-en-materia-de-prevención-de-rrll-en-el-cpd)
   - [Implementación del CPD en AWS](#implementación-del-cpd-en-aws)
     - [Servicio Web y SFTP](#servicio-web-y-sftp)
     - [Servicio LDAP / Active Directory](#servicio-ldap--active-directory)
     - [Centralización de logs y Ansible](#centralización-de-logs-y-ansible)
     - [Streaming multimedia](#streaming-multimedia)
     - [Base de datos](#base-de-datos)
     - [Backups y almacenamiento](#backups-y-almacenamiento)
     - [Automatización con Ansible](#automatización-con-ansible)
     - [Administración segura](#administración-segura)
2. [Configuración previa](#configuración-previa)
   - [Montar VPC y Red](#montar-vpc-y-red)
   - [Grupos de seguridad](#grupos-de-seguridad)
   - [Par de claves](#par-de-claves)
3. [Creación de instancias](#creación-de-instancias)
   - [Servidor WEB-SFTP](#servidor-web-sftp)
   - [Servidor LOGS-ANSIBLE](#servidor-logs-ansible)
     - [Configuración de Ansible](#configuración-de-ansible)
   - [Servidor BBDD MySQL](#servidor-bbdd-mysql)
   - [Servidor LDAP - Active Directory](#servidor-ldap--active-directory)
   - [Servidor streaming audio y video](#servidor-streaming-audio-y-video)
   - [Servidor de backups](#servidor-de-backups)
   - [IPs Estáticas para los servidores públicos, web, ansible y streaming](#ips-estáticas-para-los-servidores-públicos-web-ansible-y-streaming)
   - [Backup del servidor de BBDD](#backup-del-servidor-de-bbdd)
   - [Registros de logs](#registros-de-logs)
4. [Instalación de servicios](#instalación-de-servicios)
   - [Servicio Audio](#servicio-audio)
   - [Servicio Video](#servicio-video)
   - [Servicio Videoconferencia](#servicio-videoconferencia)
     - [Ancho de banda](#ancho-de-banda)
     - [Script para la base de datos](#script-para-la-base-de-datos)
   - [Servicio BBDD](#servicio-bbdd)
     - [Script de instalación de la BDD en Ansible](#script-de-instalación-de-la-bdd-en-ansible)
       - [Bloque 1: Configuración inicial](#bloque-1-configuración-inicial)
       - [Bloque 2: Tareas de ejecución](#bloque-2-tareas-de-ejecución)
       - [Bloque 3: Configuración final](#bloque-3-configuración-final)
     - [Script de creación de usuarios para la BDD](#script-de-creación-de-usuarios-para-la-bdd)
   - [Servicio Web](#servicio-web)
   - [Servicio SFTP](#servicio-sftp)

---

# Propuesta del CPD

## Ubicación física

### Situación física de la sala del edificio

> 📍 [Ubicación en Google Maps — STUDIO52 Bcn, Carrer de la Ciutat de Granada, 52](https://www.google.com/maps/place/STUDIO52+Bcn+%7C+Coworking+%26+Estudio+Fotogr%C3%A1fico/@41.3965489,2.1949911,15z/)

El CPD estará ubicado en una sala independiente dentro de la oficina situada en **Carrer de la Ciutat de Granada, 52**, en el distrito tecnológico de Sant Martí, una zona adecuada para empresas tecnológicas por su buena conectividad y acceso a servicios de telecomunicaciones.

La sala se encontrará alejada de las zonas de trabajo y de paso frecuente de empleados o clientes. Esta ubicación se ha seleccionado para mejorar la seguridad física, reducir el ruido de los servidores y facilitar el control ambiental de la infraestructura.

La sala estará diseñada exclusivamente para alojar los equipos críticos de la empresa (servidores, switches y sistemas de almacenamiento) y contará con **acceso restringido únicamente al personal autorizado**.

Para aumentar la seguridad, la sala **no estará señalizada** como "CPD" ni como "Sala de servidores", evitando así llamar la atención o facilitar la identificación de la infraestructura crítica.

El acceso se realizará mediante un **sistema de control con tarjetas RFID y cerradura electrónica**. Todos los accesos quedarán registrados automáticamente para mantener un control de entradas y salidas del personal autorizado.

---

### Sistema de climatización

La sala dispondrá de un sistema de climatización independiente mediante un aire acondicionado instalado en la pared del CPD, dedicado exclusivamente a la refrigeración de la sala de servidores.

- **Temperatura:** entre **20 °C y 22 °C** para evitar sobrecalentamientos.
- **Humedad relativa:** entre el **45% y el 50%**, evitando electricidad estática o condensación.

El funcionamiento es el siguiente: el aire frío circulará hacia la parte **frontal** de los racks, los servidores lo captarán para refrigerarse y el aire caliente se expulsará por la parte **trasera**, creando una circulación continua.

El sistema contará con **filtros de aire** para reducir la acumulación de polvo y proteger los componentes electrónicos.

---

### Medidas para dificultar la identificación de la sala

Para mejorar la seguridad física del CPD, la sala no tendrá señalización visible y exteriormente tendrá apariencia de cuarto técnico o almacén interno.

Además del control de acceso RFID, la sala contará con:

- Videovigilancia 24/7
- Registro de accesos
- Puerta de seguridad reforzada
- Sensores de apertura de puerta

---

### Distribución y gestión del cableado

Toda la instalación de cableado estará organizada de forma estructurada para facilitar el mantenimiento y futuras ampliaciones.

- El cableado de red se distribuirá mediante **canaletas amarillas** visibles en el plano de la oficina, desde cada puesto de trabajo hasta el CPD.
- El recorrido principal discurrirá por el **techo técnico**, bajando mediante canaletas hacia los puestos y dispositivos de red.
- El cableado del sistema de climatización estará identificado con **canaletas rojas**.
- Todos los cables estarán **etiquetados** y conectados directamente a los patch panels y switches del rack de comunicaciones.
- El **cableado eléctrico y de red estarán separados** para evitar interferencias electromagnéticas.
- Se utilizará cableado **Cat6A** para velocidades Gigabit y preparación para futuras ampliaciones.

---

### Suelo técnico y techo técnico

La oficina dispondrá de **techo técnico / falso techo** principalmente para el paso del cableado estructurado y parte de la instalación eléctrica.

A través del techo técnico se instalarán:

- Cableado de red (canaletas amarillas)
- Cableado del sistema de climatización (canaletas rojas)
- Iluminación LED
- Sensores antiincendios
- Conductos de ventilación

Debido al tamaño de la sala del CPD y al tipo de oficina, **no será necesario un suelo técnico elevado completo**. Dentro del CPD sí se utilizarán canalizaciones organizadas y espacio suficiente para facilitar la ventilación y el mantenimiento de los racks.

---

### Plano

El diagrama muestra la distribución física de las instalaciones de InnovateTech y la ubicación del CPD. Se distinguen diferentes zonas: oficina principal, baño, sala de descanso y almacén. En la parte derecha se encuentra el CPD, separado del resto de áreas para mejorar la seguridad y el control de acceso.

El esquema también representa el recorrido del cableado de red desde el CPD hacia las distintas zonas de trabajo de la oficina, permitiendo centralizar la infraestructura tecnológica y facilitar la administración de servidores, comunicaciones y conexiones de red.

---

### Estructuración de los racks

El CPD contará con **dos racks** adaptados al tamaño real de la infraestructura de la empresa.

#### Rack 1 – Comunicaciones y red (12U)

Rack dedicado a toda la infraestructura de red y comunicaciones:

| Componente | Descripción |
|---|---|
| 1 Patch Panel Cat6A | Centraliza todas las conexiones de red |
| 1 Switch gestionable 48 puertos | Soporte VLAN |
| 1 Firewall pfSense | Protección y segmentación de red |
| 1 Router | Conexión a Internet |
| Organizadores horizontales | Gestión del cableado |
| 1 SAI/UPS 3U | Protección eléctrica |

#### Rack 2 – Servidores y almacenamiento (22U)

Rack destinado a alojar los servidores principales y el sistema de almacenamiento:

| Componente | Descripción |
|---|---|
| Servidor Web + SFTP | Servicio web y transferencia segura |
| Servidor Active Directory y LDAP | Gestión de usuarios y autenticación |
| Servidor centralización de logs | Auditoría y monitorización |
| Servidor de monitorización | Control de infraestructura |
| Servidor multimedia | Streaming de audio y vídeo |
| NAS — RAID 5 | Copias de seguridad |
| 1 SAI/UPS 3U | Alimentación redundante |
| Espacios reservados | Ventilación y futuras ampliaciones |

---

## Infraestructura IT

> 📊 [Especificaciones del CPD — Google Sheets](https://docs.google.com/spreadsheets/d/1MzhewkMIZfSg18bx69DwVxc5Ksz98NR3uOj41DazYLU/edit?usp=drive_link)

### Servidores

La infraestructura del CPD estará formada por **seis servidores físicos profesionales** montados en rack, conectados mediante red Gigabit y fibra óptica interna.

| Servidor | Modelo | Servicio |
|---|---|---|
| Servidor 1 | Dell PowerEdge R250 | Web |
| Servidor 2 | Dell PowerEdge R360 | Active Directory |
| Servidor 3 | HPE ProLiant DL380 Gen11 | Streaming multimedia |
| Servidor 4 | Dell PowerEdge R450 | Comunicaciones y monitorización |
| Servidor 5 | Dell PowerEdge R450 | Base de datos |
| Servidor 6 | Dell PowerEdge R760 | NAS y copias de seguridad |

---

#### Servidor 1 – Web

**Modelo:** Dell PowerEdge R250 (1U)  
**CPU:** Intel Xeon E-2334 | **RAM:** 8 GB DDR4 | **Almacenamiento:** SSD SATA 960 GB

Servicios alojados:
- Página web
- Servicio SFTP

---

#### Servidor 2 – Active Directory

**Modelo:** Dell PowerEdge R360 (1U)  
**CPU:** Intel Xeon E-2434 | **RAM:** 16 GB DDR5 | **Almacenamiento:** SSD 960 GB

Servicios gestionados:
- Usuarios y autenticación
- Políticas de grupo
- LDAP
- Permisos de acceso

---

#### Servidor 3 – Streaming multimedia

**Modelo:** HPE ProLiant DL380 Gen11 (2U)  
**CPU:** Intel Xeon Silver 4510 | **RAM:** 32 GB DDR5  
**Almacenamiento:** SSDs para sistema + HDDs 4 TB para multimedia

Servicios:
- Streaming de audio y vídeo
- Almacenamiento multimedia
- Servicios multimedia internos

---

#### Servidor 4 – Comunicaciones y monitorización

**Modelo:** Dell PowerEdge R450 (1U)  
**CPU:** Doble Intel Xeon Silver 4314 | **RAM:** 64 GB DDR4

Servicios:
- Monitorización de infraestructura
- Centralización de logs
- Herramientas de análisis y control de red
- Supervisión de servidores, temperatura, consumo, red y almacenamiento

---

#### Servidor 5 – Base de datos

**Modelo:** Dell PowerEdge R450 (1U)  
**CPU:** Intel Xeon Gold 5317 | **RAM:** 64 GB DDR4 | **Almacenamiento:** SSD (lectura/escritura optimizada)

Servidor dedicado exclusivamente al servicio de bases de datos para garantizar:
- Mayor rendimiento y estabilidad
- Seguridad de la información

---

#### Servidor 6 – NAS y backups

**Modelo:** Dell PowerEdge R760 (2U)  
**CPU:** Intel Xeon Silver 4410T | **RAM:** 64 GB DDR5  
**Almacenamiento:** SSDs para sistema + 8 × HDD 6 TB (RAID 5)

Servicios:
- Backups automáticos y almacenamiento centralizado
- Recuperación de datos
- Copias de seguridad de máquinas virtuales y bases de datos

---

### Patch panels

Se instalarán en el rack de comunicaciones:

- **2 Patch panels Ethernet Cat6A** de 24 puertos
- **2 Patch panels de fibra óptica duplex**

Todos los puestos de trabajo estarán conectados directamente al CPD mediante cableado estructurado distribuido a través del techo técnico.

---

### Switches

Se utilizarán **dos switches gestionables TP-Link TL-SG1428PE V2.20** con las siguientes características:

- 26 puertos RJ45 Gigabit
- 2 puertos SFP Gigabit
- Soporte VLAN y QoS
- Administración centralizada
- Capacidad de conmutación: **56 Gbps**

---

### Router y Access Point

| Dispositivo | Modelo | Función |
|---|---|---|
| Router | Reyee RG-EG3105P-E | Segmentación de red, gestión WAN, conectividad externa, protección básica |
| Access Point | TP-Link EAP723 | Conectividad WiFi de alta velocidad |

---

### Diagramas y distribución

El diagrama muestra la infraestructura física de InnovateTech organizada en dos racks principales:

- **Rack 1 (Comunicaciones y red):** patch panels, organizadores de cableado, switch principal, firewall pfSense, router y SAI/UPS.
- **Rack 2 (Servidores y almacenamiento):** servidores web, Active Directory, bases de datos SQL, monitorización, almacenamiento NAS para backups y espacio reservado para futuras ampliaciones.

Ambos racks cuentan con sistemas de alimentación protegida y una distribución estructurada que facilita la gestión, mantenimiento y escalabilidad de la infraestructura.

---

## Infraestructura eléctrica

### Sistemas de alimentación redundante

Todos los servidores y equipos de comunicaciones estarán conectados a **sistemas SAI online Eaton**. La distribución eléctrica estará separada entre el rack de comunicaciones y el rack de servidores.

---

### SAIs

El CPD utilizará:

- **1 Eaton 9PX 9PX5KIRTN** de 5000 VA
- **2 módulos de baterías Eaton 9PX EBM**

| Parámetro | Valor |
|---|---|
| Potencia total estimada | ✅ 3720 VA |
| Consumo total estimado | ✅ 2575 W |
| Autonomía estimada | ~25 – 35 minutos |

Para el cálculo de capacidad se ha aplicado: factor de seguridad, margen de crecimiento y eficiencia energética.

La autonomía permite:
- Mantener servicios activos
- Realizar apagado controlado
- Evitar pérdida de datos
- Proteger bases de datos y máquinas virtuales

---

### Distribución eléctrica

Cada rack contará con:

- PDU independiente
- Alimentación protegida
- Distribución organizada de corriente

Los servidores con **doble fuente de alimentación** estarán conectados a líneas redundantes diferentes para garantizar alta disponibilidad ante fallos eléctricos parciales.

---

## Seguridad física y lógica

### Seguridad física

#### Control de acceso

Se instalará una **cerradura electrónica de seguridad** en la puerta de acceso al CPD con los siguientes métodos de autenticación:

- Huella dactilar
- Código PIN
- Tarjeta RFID / tag NFC

Funciones adicionales:
- Apertura remota
- Timbre integrado
- Registro de accesos

> 🔗 [Cerradura inteligente EZVIZ CS-DL05](https://www.pccomponentes.com/cerradura-inteligente-ezviz-cs-dl05-wifi-huella-dactilar-codigo-pin-apertura-remota)

---

#### Videovigilancia

Se instalará una **cámara de seguridad con cobertura 360°** y detección de movimiento para supervisar continuamente el acceso y el interior del CPD.

La cámara:
- Enviará alertas al teléfono móvil ante actividad sospechosa
- Mantendrá grabación continua como evidencia

> 🔗 [Cámara Hiseeu WHC905 5MP PTZ](https://www.hiseeu.com/en-eu/products/security-camera-5mp-ptz-whc905)

---

#### Sensor de movimiento

Se instalará un **sensor Ajax MotionProtect Plus** (tecnología PIR + microondas) con las siguientes capacidades:

- Detección de movimiento hasta **12 metros**
- Protección antisabotaje (tamper)
- Comunicación inalámbrica con la central Ajax
- Avisos instantáneos al sistema de alarma
- Supervisión automática del estado del dispositivo

> 🔗 [Ajax MotionProtect Plus](https://www.securame.com/aj-motionprotectplus-w-detector-volumetrico-pir-ajax-anti-mascotas-doble-tecnologia-p-2899.html)

---

#### Sensor de apertura de puerta

La puerta del CPD contará con un **sensor de apertura** conectado al sistema de seguridad, capaz de detectar:

- Aperturas no autorizadas
- Intentos de manipulación
- Accesos fuera del horario permitido

En caso de detección, el sistema enviará **alertas automáticas al móvil** de los administradores y quedará registrado en el sistema de monitorización.

> 🔗 [Alarma Nivian WiFi con sensor magnético](https://www.pccomponentes.com/alarma-nivian-wifi-inalambrica-sensor-magnetico-interior-sirena-100db-pack-3)

---

#### Sensor de fuga de agua

Se instalará un **sensor de detección de agua** para prevenir daños por inundación o fugas. El sistema enviará alertas mediante:

- SMS
- Correo electrónico
- Llamadas
- Dashboard web

> 🔗 [WLD2 Detector de fugas de agua](https://rivertic.com/producto/wld2-detector-de-fugas-de-agua/)

---

#### Control de temperatura y humedad

Se instalarán **varios sensores distribuidos** por la sala para garantizar condiciones ambientales óptimas y evitar sobrecalentamientos o problemas de condensación.

> 🔗 [TFA View Climate Center](https://www.thomann.es/tfa_view_climate_center.htm)

---

#### Detección y extinción de incendios

La sala dispondrá de:

- **Detectores de humo** cableados de alta sensibilidad conectados al sistema de alarmas
- **Extintor de CO₂ 5 kg** para incendios eléctricos
- **Sistema automático de extinción mediante gas Novec 1230**

Características del gas Novec 1230:
- No daña componentes electrónicos
- No conduce electricidad
- No deja residuos
- Es seguro para personas

El sistema podrá activarse:
- Automáticamente mediante detección de humo o calor extremo
- Manualmente mediante pulsador de emergencia

> 🔗 [Extintor CO₂ 5 kg](https://extintorescontraincendios.com/extintores-co2/extintor-co2-5kg-cuadros-electricos-28.html)

---

#### Climatización

La refrigeración del CPD se realizará mediante un **aire acondicionado de pared** preparado para funcionamiento continuo **24/7**, manteniendo temperatura estable para proteger servidores y dispositivos de red frente al sobrecalentamiento.

---

#### Vías de evacuación

La sala contará con:

- Iluminación de emergencia
- Acceso despejado
- Espacio suficiente entre racks
- Ausencia de obstáculos en la salida

Esto facilitará tanto la evacuación como las tareas de mantenimiento de los técnicos.

---

#### Plano de seguridad física

El plano de seguridad física representa la distribución de los sistemas de protección en todas las zonas de la empresa (oficinas, almacén, pasillos y CPD).

**Medidas en el CPD:**
- Detectores de humo
- Sistema automático de extinción de incendios
- Cámara de videovigilancia
- Sensor de apertura en la puerta

**Medidas en zonas comunes:**
- Extintores
- Cámaras de seguridad
- Sensores de movimiento
- Salida de emergencia señalizada

---

### Seguridad lógica

#### Restricción de acceso por autorización

Todos los servidores utilizarán **autenticación mediante claves SSH públicas y privadas**, eliminando completamente el acceso por contraseña para reducir riesgos de ataques de fuerza bruta.

La infraestructura contará con un **servidor LDAP** que centralizará:
- Usuarios y grupos
- Permisos y autenticación

El **Servidor 2 (LDAP)** se ha desplegado en la zona privada de la VPC, actuando como el corazón de la autorización de la empresa y evitando cuentas locales descontroladas.

---

#### Firewalls y segmentación de red

La red se dividirá en dos zonas lógicas dentro de la VPC:

**Subred pública** — Servidores con IP pública accesibles desde Internet:

| Servidor | Función |
|---|---|
| Servidor 1 | Web / SFTP |
| Servidor 3 | Streaming |
| Servidor 4 | Logs / Ansible |

**Subred privada** — Servidores sin IP pública, solo accesibles por la red interna:

| Servidor | Función |
|---|---|
| Servidor 2 | LDAP |
| Servidor 5 | Base de datos |
| Servidor NAS | Backup |

---

#### AWS Security Groups

La infraestructura utilizará grupos de seguridad configurados con política de **"denegación por defecto" (Default Deny)**.

Grupo creado: `administracion-security-iner`

Reglas principales:

| Puerto | Protocolo | Descripción |
|---|---|---|
| 22 | SSH | Permitido solo para administración remota autorizada |
| 3306 | MySQL | Accesible solo desde la IP privada del servidor web |

---

#### Monitorización

El servidor **Logs-Ansible** actuará como sistema centralizado de monitorización y auditoría, recopilando:

- Logs del sistema
- Eventos de seguridad
- Intentos de acceso fallidos
- Estado de servicios

---

#### Copias de seguridad / Backups

- Las copias de seguridad se realizarán **automáticamente de forma diaria** y se almacenarán en el servidor NAS independiente.
- Se realizarán también **backups externos en AWS** para recuperación ante desastres.

Los backups incluirán:
- Máquinas virtuales
- Bases de datos
- Configuraciones de red
- Archivos críticos de la empresa

---

#### RAIDs

- El servidor NAS utilizará **RAID 5** para proporcionar redundancia y tolerancia a fallos.
- AWS proporciona redundancia física sobre los **volúmenes EBS** utilizados por las instancias EC2.

---

## Prevención de riesgos laborales

### Medidas aplicadas en materia de prevención de RRLL en el CPD

La sala contará con:

- Correcta ventilación y climatización
- Iluminación adecuada
- Suelo antiestático
- Cableado organizado mediante canaletas
- Separación entre líneas eléctricas y de red
- Extintores accesibles
- Espacio suficiente para trabajar de forma segura

Se realizarán **revisiones periódicas** de:
- Climatización
- Sistemas eléctricos y baterías SAI
- Sistemas antiincendios
- Estado general de racks y servidores

---

## Implementación del CPD en AWS

La infraestructura del CPD también contará con una implementación en la nube mediante **AWS EC2**. Todas las máquinas virtuales se han desplegado manualmente utilizando instancias Linux sin software preinstalado.

| Instancia AWS | Función |
|---|---|
| Servidor1-Web-SFTP | Servicio Web y SFTP |
| Servidor-2-LDAP | Active Directory / LDAP |
| Servidor4-Logs-Ansible | Centralización de logs y Ansible |
| Servidor-3-Streaming | Streaming multimedia |
| Servidor-5-BaseDatos | Base de datos |
| Servidor-NAS-Backup | Backups y almacenamiento |

---

### Servicio Web y SFTP

La instancia **Servidor1-Web-SFTP** alojará:

- Página web corporativa y panel de administración para la base de datos
- Servicio SFTP

El servidor web funcionará mediante **Nginx sobre Linux**. El servicio SFTP estará integrado con el servidor LDAP para centralizar usuarios y permisos.

---

### Servicio LDAP / Active Directory

La instancia **Servidor-2-LDAP** gestionará:

- Usuarios y grupos
- Autenticación y permisos

Este servidor centralizará el acceso al resto de servicios de la infraestructura.

---

### Centralización de logs y Ansible

La instancia **Servidor4-Logs-Ansible** tiene doble función:

1. **Centralización de logs** de servidores, firewall, servicios de red y sistemas Linux
2. **Automatización mediante Ansible** para configuraciones y despliegues en otras máquinas virtuales

---

### Streaming multimedia

La instancia **Servidor-3-Streaming** está dedicada a los servicios multimedia de audio y vídeo (streaming interno, contenidos multimedia y servicios audiovisuales).

---

### Base de datos

La instancia **Servidor-5-BaseDatos** aloja el sistema gestor de bases de datos, separada del resto de servicios para mejorar seguridad, rendimiento, estabilidad y administración.

---

### Backups y almacenamiento

La instancia **Servidor-NAS-Backup** almacena:

- Copias de seguridad y archivos críticos
- Snapshots y backups automáticos

Esta separación evita la pérdida total de datos en caso de fallo de otros servidores.

---

### Automatización con Ansible

Las máquinas automatizadas con Ansible son:

- `Servidor-2-LDAP`
- `Servidor-5-BaseDatos`

Tareas automatizadas:
- Instalación de paquetes
- Configuración de servicios
- Creación de usuarios y configuración de permisos
- Despliegue de configuraciones
- Actualización de sistemas
- Configuración SSH

Todos los playbooks utilizados quedarán documentados para facilitar la administración y mantenimiento.

---

### Administración segura

Todas las instancias se administrarán mediante **usuarios personalizados** (sin usar el usuario por defecto del sistema).

El acceso remoto se realizará exclusivamente mediante **autenticación SSH con clave pública y privada**, deshabilitando el acceso por contraseña.

Cada servidor contará con:
- Firewall configurado
- Permisos restringidos
- Monitorización de accesos
- Actualización periódica de seguridad

---

# Configuración previa

## Montar VPC y Red

Lo primero es crear una **VPC** (Virtual Private Cloud — red privada y aislada dentro de la infraestructura de nube) que nos permite controlar la red: selección de direcciones IP, subredes, tablas de enrutamiento y acceso a Internet.

Para crearla: ir a **VPC** → **Crear VPC**.

Se elige un rango que proporcione **65.536 direcciones IP**, dando espacio suficiente para estructurar la red sin quedarnos sin IPs.

Se crean:

- **2 subredes públicas** — para servidores accesibles directamente desde Internet (servidor Web, SFTP).
- **2 subredes privadas** — para proteger recursos críticos como la Base de Datos o el servidor de Logs, impidiendo acceso directo desde Internet.

Las máquinas en subredes privadas podrán salir a Internet para descargar actualizaciones, pero nadie desde fuera podrá acceder a ellas.

---

## Grupos de seguridad

El grupo de seguridad actúa como **firewall** que controla el tráfico de red entrante (inbound) y saliente (outbound).

Para crearlo: ir a **EC2** → **Security Groups**.

Configuración aplicada:

- **Regla de entrada:** se limita el acceso SSH (puerto 22) exclusivamente a `Mi IP`, aplicando el **principio de mínimo privilegio**. Aunque un atacante descubriera la IP pública del servidor, AWS descartará todo su tráfico en el cortafuegos perimetral.
- **Regla de salida:** se mantiene la regla por defecto para que los servidores puedan comunicarse con Internet.

> ⚠️ Las reglas se fueron ajustando a medida que avanzó el proyecto.

---

## Par de claves

Para evitar el acceso por contraseña (y así cumplir los requisitos de seguridad), es necesario crear un **par de claves criptográficas**.

Desde **EC2** → **Pares de claves**:

Se genera un par de claves **RSA en formato `.pem`**, garantizando:
- Acceso SSH automatizable
- Deshabilitar por completo la autenticación por contraseñas

---

# Creación de instancias

## Servidor WEB-SFTP

La creación de este servidor se realiza mediante el entorno gráfico de AWS.

Configuración:
- **SO:** Ubuntu Server (AMI por defecto)
- **Tipo de instancia:** `t2.micro` (nivel gratuito, ideal para baja demanda de CPU)
- **Par de claves:** el generado anteriormente
- **VPC:** la VPC creada previamente
- **Subred:** subred pública con IP pública habilitada
- **Grupo de seguridad:** el creado previamente + reglas de entrada HTTP y HTTPS
- **Almacenamiento:** ~15 GB (SO ~4-5 GB + ~500 MB web + ~9-10 GB exclusivos para SFTP)

---

## Servidor LOGS-ANSIBLE

El proceso es análogo al del servidor WEB-SFTP. Este es la **máquina cerebro** desde la que se realizarán todas las automatizaciones con Ansible.

- Se selecciona la **otra subred pública** para alta disponibilidad.
- **Almacenamiento:** 20 GB (recibirá logs de todos los servidores del grupo y alojará Jitsi).

---

### Configuración de Ansible

Para trabajar con Ansible es necesario instalarlo en este servidor:

```bash
# Instalación de Ansible
sudo apt update && sudo apt install ansible -y

# Verificación
ansible --version
```

Pasos adicionales:

```bash
# Crear carpeta de trabajo para Ansible
mkdir ~/ansible && cd ~/ansible

# Instalar repositorios de AWS (boto3, botocore)
pip install boto3 botocore

# Generar clave pública a partir de la clave privada .pem
ssh-keygen -y -f clave.pem > clave.pub
```

Se crea el archivo `hosts` con las IPs privadas de los servidores. Este archivo actúa como el mapa de la infraestructura, permitiendo que el servidor automatice, configure y audite todos los servidores de forma segura a través de la red interna.

```bash
# Ejecutar con confianza total en la red privada (sin verificar fingerprints SSH)
ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook -i hosts --private-key clave.pem playbook.yml
```

Playbook para crear el grupo `administradores`, el usuario `admin-innovate` y configurar sudo sin contraseña:

```bash
# Verificación del funcionamiento
ansible all -i hosts -m ping --private-key clave.pem

# Acceso con el nuevo usuario
ssh -i clave.pem admin-innovate@<IP>

# Bloqueo de contraseñas
sudo passwd -l admin-innovate
```

---

## Servidor BBDD MySQL

Para desplegar MySQL mediante Ansible, primero se crea un **playbook** que:

1. Actualiza los repositorios del sistema
2. Cambia la configuración de MySQL para aceptar peticiones externas
3. Crea la base de datos con sus tablas y usuario

**Dependencias necesarias para que Ansible interactúe con AWS:**

- **Botocore:** biblioteca Python con el mapa de herramientas de AWS
- **Boto3:** SDK oficial de Amazon para Python

```bash
pip install botocore boto3
```

Se crea el fichero de despliegue de la instancia (AMI, grupo de seguridad, región, nombre, clave, VPC).

```bash
# Exportar credenciales AWS temporales
export AWS_ACCESS_KEY_ID="..."
export AWS_SECRET_ACCESS_KEY="..."
export AWS_SESSION_TOKEN="..."

# Ejecutar el playbook de creación de instancia
ansible-playbook crear-instancia-bbdd.yml

# Añadir IP privada al fichero hosts (ejemplo: 10.0.128.60)
# Ejecutar el playbook de instalación del servicio MySQL
ansible-playbook -i hosts instalar-mysql.yml --private-key clave.pem

# Verificar que la base de datos fue creada
mysql -u root -e "SHOW DATABASES;"
```

---

## Servidor LDAP - Active Directory

El proceso de creación de la instancia es idéntico al del servidor de BBDD (mismos parámetros: clave, AMI, VPC, grupo de seguridad, nombre y tipo de instancia).

El playbook de Ansible realiza:

1. Instalación de **OpenLDAP**
2. Definición del dominio
3. Actualización de repositorios
4. Configuración del dominio y creación de objetos LDAP

```bash
# Despliegue automático con Ansible
ansible-playbook -i hosts instalar-ldap.yml --private-key clave.pem

# Verificación del dominio y los objetos creados
ldapsearch -x -H ldap://localhost -b "dc=innovatetech,dc=local"
```

---

## Servidor streaming audio y video

El proceso de creación de la instancia es el mismo que para el resto de servidores.

- Se añade **mayor cantidad de disco** (30 GB) dado que el servicio de streaming requiere almacenamiento adicional.
- Se lanza la instancia y se copia la IP privada para añadirla al servidor central.

---

## Servidor de backups

Se implementa un **RAID 5 por software** para el servidor NAS. Al ser un servidor de almacenamiento aislado, **no se asigna IP pública**.

---

## IPs Estáticas para los servidores públicos, web, ansible y streaming

Se asignan **Elastic IPs (IPs estáticas)** a los servidores que necesitan ser accesibles de forma consistente desde Internet:

- Servidor Web
- Servidor Ansible/Logs
- Servidor Streaming

---

## Backup del servidor de BBDD

Para implementar el **RAID 5** se necesitan un total de **3 discos adicionales**:

**Desde EC2 → Volúmenes (EBS):**

1. Crear 3 volúmenes de 5 GB cada uno (tamaño de prueba para el proyecto).
2. Asociar los 3 volúmenes al servidor NAS.

Desde el servidor Ansible, se automatiza la configuración del RAID 5 por software con un playbook:

```bash
ansible-playbook -i hosts configurar-raid5.yml --private-key clave.pem

# Verificación
cat /proc/mdstat
```

> **Nota:** RAID 5 utiliza el tamaño equivalente a 1 disco para paridad. Por tanto: `5 GB × (3 - 1) = 10 GB` de espacio útil.

**Backups automatizados:**

- En el **Servidor BBDD:** se crea un script que realiza un volcado (`dump`) de la base de datos `bd_innovate` y guarda el archivo `.sql` localmente.
- En el **Servidor NAS:** se crea un cron job que recoge el archivo comprimido por la red privada (SSH/SCP) y lo guarda en el volumen RAID 5 (`/nas/backups`).

```bash
# Verificar el script generado por Ansible
cat /usr/local/bin/backup_db.sh

# Forzar ejecución manual del script para prueba real
sudo /usr/local/bin/backup_db.sh

# Forzar la recolección manual en el NAS
sudo /usr/local/bin/recoger_backup.sh

# Comprobar que el archivo .sql.gz está en el directorio RAID 5
ls -lh /nas/backups/
```

El archivo comprimido `.sql.gz` se aloja correctamente dentro de `/nas/backups`, montado sobre el volumen RAID 5.

---

## Registros de logs

Se configura el envío centralizado de logs de todos los servidores hacia el servidor Logs-Ansible mediante **rsyslog**.

```bash
# Añadir regla de entrada en el grupo de seguridad del servidor de logs (puerto 514 UDP/TCP)

# Forzar prueba de envío de log desde un servidor cliente
logger -n <IP_LOGS_SERVER> -P 514 "Test log desde servidor X"

# Verificación en el servidor de logs
tail -f /var/log/syslog | grep "Test"
```

**Comandos útiles de MySQL para verificaciones:**

```sql
USE bd_innovate;
SHOW TABLES;
TRUNCATE TABLE control_copias_seguridad;
SELECT * FROM control_copias_seguridad;
ALTER EVENT copia_seguridad_diaria_critica ON SCHEDULE EVERY 1 DAY STARTS CURRENT_TIMESTAMP;
SELECT * FROM control_copias_seguridad;
```

```bash
ls /var/lib/mysql-files/backups
```

---

# Instalación de servicios

## Servicio Audio

Para el servicio de radio se utilizan:

- **Icecast2:** servidor de streaming de audio de código abierto
- **Liquidsoap:** cliente que envía el flujo de audio a Icecast2

```bash
# Actualizar repositorios
sudo apt update && sudo apt upgrade -y

# Cambiar el nombre de la máquina
sudo hostnamectl set-hostname streaming-server
sudo reboot

# Instalar Icecast2
sudo apt install icecast2 -y
```

Durante la instalación se solicitarán tres contraseñas:
- Contraseña de source (para compartir recursos): `Jn542aH7NFGI83J6XS3k`
- Contraseña de relay: `3gP78Yw9NqYvqR6GUItp`
- Contraseña de administración: `PPW3nf49W4z3PAlxuX5Z`

```bash
# Habilitar Icecast2 en /etc/default/icecast2
sudo nano /etc/default/icecast2
# Añadir: ENABLE=true

# Iniciar y habilitar el servicio
sudo systemctl start icecast2
sudo systemctl enable icecast2
sudo systemctl status icecast2

# Crear directorio de música y descargar canciones de prueba
sudo mkdir /music
cd /music
# (descargar archivos de audio de prueba)

# Instalar Liquidsoap
sudo apt install liquidsoap -y
```

Crear el fichero de configuración de Liquidsoap (`/etc/liquidsoap/radio.liq`):

```bash
# La contraseña del apartado "password" debe coincidir con la primera contraseña de Icecast2

# Crear fichero de log y asignar permisos
sudo touch /var/log/liquidsoap/radio.log
sudo chmod 644 /var/log/liquidsoap/radio.log

# Ejecutar Liquidsoap
liquidsoap /etc/liquidsoap/radio.liq
```

Acceso a Icecast2 en el navegador:

```
http://52.70.15.98:8000
```

Para conectarse mediante VLC: **Soporte multimedia** → **Abrir flujo de red** → introducir la URL del stream.

---

## Servicio Video

Se utiliza **Nginx con el módulo RTMP** para transmitir vídeo en directo.

```bash
# Instalar Nginx con módulo RTMP
sudo apt install nginx libnginx-mod-rtmp -y

# Hacer backup del fichero de configuración
sudo cp /etc/nginx/nginx.conf /etc/nginx/nginx.conf.bak
```

Añadir el módulo RTMP fuera del bloque `http` en `/etc/nginx/nginx.conf`:

```nginx
rtmp {
    server {
        listen 1935;
        application live {
            live on;
            hls on;
            hls_path /var/www/hls;
        }
    }
}
```

```bash
# Crear fichero de configuración del sitio web
sudo nano /etc/nginx/sites-available/streaming

# Habilitar el sitio
sudo ln -s /etc/nginx/sites-available/streaming /etc/nginx/sites-enabled/

# Verificar sintaxis
sudo nginx -t

# Crear directorio y archivo del reproductor (index.html)
sudo mkdir -p /var/www/streaming
sudo nano /var/www/streaming/index.html

# Reiniciar Nginx
sudo systemctl restart nginx
```

Configuración en **OBS Studio**:
- Ir a **Configuración** → **Directo**
- Servidor: `rtmp://52.70.15.98:1935/live`
- Codificación: Software (x264)
- Fuente: XShm (captura de pantalla)

---

## Servicio Videoconferencia

Se utiliza **Jitsi Meet** (plataforma gratuita y de código abierto para videollamadas).

```bash
# Descargar e instalar la clave pública oficial de Jitsi
curl https://download.jitsi.org/jitsi-key.gpg.key | sudo gpg --dearmor -o /usr/share/keyrings/jitsi-keyring.gpg

# Añadir el repositorio de Jitsi
echo "deb [signed-by=/usr/share/keyrings/jitsi-keyring.gpg] https://download.jitsi.org stable/" | sudo tee /etc/apt/sources.list.d/jitsi-stable.list

# Actualizar repositorios e instalar Jitsi Meet
sudo apt update
sudo apt install jitsi-meet -y
```

Durante la instalación:
- **Dominio:** introducir la IP del servidor
- **Certificado:** generar autocertificado (producirá un aviso de seguridad en el navegador)

```bash
# Verificar el estado de los servicios
sudo systemctl status jitsi-videobridge2
sudo systemctl status prosody
sudo systemctl status jicofo
```

> ⚠️ Al acceder desde el navegador aparecerá un aviso de certificado no confiable. Clicar en **Avanzado** → **Aceptar el riesgo** para continuar.

---

### Ancho de banda

Para medir el impacto de los servicios en el ancho de banda se utiliza **speedtest-cli**:

```bash
# Instalar speedtest-cli
sudo apt install speedtest-cli -y

# Medir sin servicios activos
sudo systemctl stop icecast2 nginx jitsi-videobridge2
speedtest

# Medir con servicios activos
sudo systemctl start icecast2 nginx jitsi-videobridge2
speedtest
```

Los resultados muestran un impacto aceptable en la subida y descarga, dentro de niveles completamente normales para este tipo de servicios.

---

### Script para la base de datos

Se crean scripts en Python para trasladar a la base de datos información del servidor de streaming (ancho de banda, latencia y registros de llamada).

```bash
# Instalar Python y el conector MySQL
sudo apt install python3 python3-pip -y
pip3 install mysql-connector-python
```

---

## Servicio BBDD

> **Nota:** Las primeras capturas del proceso se realizaron en un servidor de pruebas en el entorno ISARD, no en el servidor final del proyecto. Los comandos de instalación son idénticos.

```bash
# Instalación del servicio MySQL
sudo apt install mysql-server -y

# Añadir repositorio de Ansible
sudo add-apt-repository --yes --update ppa:ansible/ansible

# Instalar Ansible
sudo apt install ansible -y

# Instalar repositorio AWS para Ansible
pip3 install boto3 botocore
```

---

### Script de instalación de la BDD en Ansible

El script de Ansible que despliega el entorno MySQL se divide en **3 bloques y 16 tareas**.

---

#### Bloque 1: Configuración inicial

Define los parámetros básicos del script:

```yaml
- name: Despliegue y Configuracion Automatica de MySQL (Servidor 5)
  hosts: servidores_db
  become: yes
  gather_facts: true
```

| Parámetro | Descripción |
|---|---|
| `become: yes` | Ejecuta las tareas con privilegios elevados (sudo) |
| `gather_facts: true` | Recopila información básica de los hosts antes de ejecutar las tareas |

---

#### Bloque 2: Tareas de ejecución

Este bloque contiene todas las tareas del script. Etiquetas más importantes:

| Etiqueta | Descripción |
|---|---|
| `name` | Nombre/descripción de cada tarea |
| `ansible.builtin.copy` | Transfiere contenido local a los equipos destino |
| `ansible.builtin.shell` | Ejecuta comandos del terminal |
| `ansible.builtin.mysql_db` | Gestiona elementos de la base de datos |
| `ansible.builtin.lineinfile` | Busca y edita líneas en archivos |
| `state: present` | El recurso debe existir |
| `state: started` | El recurso debe estar iniciado |
| `become` | Define propietario del elemento |
| `mode` | Define permisos del elemento (como chmod) |

**Resumen de las 16 tareas:**

| Tarea | Descripción |
|---|---|
| 1 | Asegurar instalación y actualización de `mysql-server` y `python3-pymysql` |
| 2 | Verificar que los servicios MySQL están operativos |
| 3 | Permitir conexiones desde cualquier IP (para facilitar la integración entre servidores) |
| 4 | Crear la base de datos del proyecto |
| 5 | Crear usuario administrador inicial `iner` |
| 6 | Crear tablas con sus campos (usando `ENUM` y `CHECK` para validación de datos) |
| 7 | Leer y ejecutar el archivo `.sql` generado en la tarea 6 dentro de MySQL |
| 8 | Crear el directorio para copias de seguridad |
| 9 | Copiar el archivo `.sql` de inserción de datos al servidor |
| 10 | Ejecutar el archivo `.sql` para crear registros iniciales |
| 11 | Crear triggers de auditoría |
| 12 | Ejecutar el archivo `.sql` con los triggers |
| 13 | Habilitar y activar el Event Scheduler de MySQL |
| 14 | Crear la tarea programada de copias de seguridad diarias |
| 15 | Ejecutar el `.sql` de creación de la tarea programada |
| 16 | Crear usuarios básicos y asignar permisos según su rol |

**Estructura de los triggers de auditoría:**

Los triggers controlan:
- Cuota de minutos de llamada mensuales (límite: 600 min)
- Número máximo de llamadas diarias por usuario
- Intentos de modificación por usuarios con rol trabajador/ventas en tablas restringidas
- Acceso de empleados con rol administración a la tabla de llamadas de clientes
- Bloqueo de llamadas para usuarios bloqueados

```sql
DELIMITER $$

DROP TRIGGER IF EXISTS trigger_quota_mensual_minutos$$
CREATE TRIGGER trigger_quota_mensual_minutos
BEFORE INSERT ON registro_actividad_llamada
FOR EACH ROW
BEGIN
    DECLARE minutos_mes INT DEFAULT 0;
    SELECT IFNULL(SUM(duracion_llamada), 0) / 60 INTO minutos_mes
    FROM registro_actividad_llamada
    WHERE id_originador_llamada = NEW.id_originador_llamada
      AND MONTH(hora_inicio_llamada) = MONTH(CURRENT_DATE())
      AND YEAR(hora_inicio_llamada) = YEAR(CURRENT_DATE());
    IF minutos_mes >= 600 THEN
        INSERT INTO aviso (usuario, tabla_afectada, operacion_realizada, motivo)
        VALUES (USER(), 'registro_actividad_llamada', 'INSERT', 'Cuota de minutos mensuales superada (600 min)');
        SIGNAL SQLSTATE '45000'
        SET MESSAGE_TEXT = 'Error: Se ha superado el limite de minutos mensuales permitidos (600 min).';
    END IF;
END$$

DELIMITER ;
```

**Glosario de elementos SQL utilizados en los triggers:**

| Elemento | Descripción |
|---|---|
| `DELIMITER` | Cambia el delimitador para que MySQL no interprete `;` como fin de bloque |
| `CREATE TRIGGER` | Inicia la creación del trigger con su nombre identificativo |
| `BEFORE` | La lógica se aplica antes de que los cambios se guarden en la BD |
| `BEGIN` | Marca el inicio de la lógica del trigger |
| `DECLARE` | Variable temporal usada dentro del trigger |
| `SIGNAL SQLSTATE` | Lanza un error para frenar la acción auditada |
| `SET MESSAGE_TEXT` | Mensaje de error descriptivo que se muestra al usuario |
| `NEW` | Referencia a los nuevos datos que se quieren insertar |

**Estructura de la tarea programada de copias de seguridad diarias:**

```sql
DELIMITER $$

DROP EVENT IF EXISTS copia_seguridad_diaria_critica$$
CREATE EVENT copia_seguridad_diaria_critica
ON SCHEDULE EVERY 1 DAY
STARTS CURRENT_TIMESTAMP
DO
BEGIN
    DECLARE codigo_error INT DEFAULT 0;
    DECLARE CONTINUE HANDLER FOR SQLEXCEPTION SET codigo_error = 1;

    SET @sql_empleados = CONCAT("SELECT * INTO OUTFILE '/var/lib/mysql-files/backups/empleados_",
        DATE_FORMAT(NOW(), '%Y%m%d'), ".csv' FIELDS TERMINATED BY ',' FROM empleado");
    PREPARE sentencia1 FROM @sql_empleados;
    EXECUTE sentencia1;
    DEALLOCATE PREPARE sentencia1;

    SET @sql_llamadas = CONCAT("SELECT * INTO OUTFILE '/var/lib/mysql-files/backups/llamadas_",
        DATE_FORMAT(NOW(), '%Y%m%d'), ".csv' FIELDS TERMINATED BY ',' FROM registro_actividad_llamada");
    PREPARE sentencia2 FROM @sql_llamadas;
    EXECUTE sentencia2;
    DEALLOCATE PREPARE sentencia2;

    IF codigo_error = 0 THEN
        INSERT INTO control_copias_seguridad (tablas_incluidas, resultado)
        VALUES ('empleado, registro_actividad_llamada', 'EXITOSO');
    ELSE
        INSERT INTO control_copias_seguridad (tablas_incluidas, resultado)
        VALUES ('empleado, registro_actividad_llamada', 'FALLIDO');
    END IF;
END$$

DELIMITER ;
```

| Elemento | Descripción |
|---|---|
| `ON SCHEDULE EVERY` | Define la frecuencia de ejecución |
| `STARTS` | Define el momento de inicio |
| `DO` | Define las acciones a realizar |
| `SET @[...] = [...]` | Guarda valores en una variable |
| `FIELDS TERMINATED BY ","` | Formato CSV para los archivos de salida |
| `PREPARE` | Compila una sentencia sin ejecutarla |
| `EXECUTE` | Ejecuta una sentencia compilada previamente |
| `DEALLOCATE PREPARE` | Libera de la memoria la sentencia preparada |

---

#### Bloque 3: Configuración final

El último bloque reinicia el servicio de MySQL para que todos los cambios realizados durante las tareas se apliquen correctamente.

---

### Script de creación de usuarios para la BDD

Se ha creado un script **independiente del de despliegue** para facilitar la creación de nuevos usuarios, ya que:

- La función del script de Ansible es desplegar la BD, no gestionar usuarios
- Los datos de cada usuario son variables (nombre, contraseña, rol), lo que haría incompatible su inclusión en el script de despliegue

**Datos solicitados durante la ejecución:**

| Campo | Obligatorio |
|---|---|
| DNI del empleado | ✅ |
| Nombre de usuario | ✅ |
| Contraseña | ✅ |
| Primer apellido | ✅ |
| Segundo apellido | — |
| Teléfono | — |
| Dirección | — |
| Departamento | — |
| Rol (admin / administración / ventas / trabajador) | ✅ |

Al finalizar, el script:
1. Inserta los datos en la tabla de empleados
2. Asigna los permisos correspondientes al rol
3. Guarda un registro del usuario creado en un archivo de log externo
4. Pregunta si se desea crear otro usuario

---

## Servicio Web

```bash
# Cambiar el nombre del servidor
sudo hostnamectl set-hostname web-server

# Crear usuario administrador
sudo adduser admin-web

# Asignar permisos de sudo
sudo usermod -aG sudo admin-web

# Cambiar al nuevo usuario
su - admin-web

# Actualizar paquetes
sudo apt update && sudo apt upgrade -y

# Instalar Nginx
sudo apt install nginx -y

# Comprobar estado del servicio
sudo systemctl status nginx
```

Acceso desde el cliente para comprobar la carga de la página:
```
http://100.49.223.120
```

```bash
# Instalar PHP
sudo apt install php php-fpm -y

# Crear directorio de la página web
sudo mkdir -p /var/www/innovatetech

# Asignar propietario y permisos
sudo chown -R www-data:www-data /var/www/innovatetech
sudo chmod -R 755 /var/www/innovatetech

# Crear archivo PHP de la página web
sudo nano /var/www/innovatetech/index.php

# Crear archivo de configuración del sitio en Nginx
sudo nano /etc/nginx/sites-available/innovatetech

# Activar el sitio y eliminar el sitio por defecto
sudo ln -s /etc/nginx/sites-available/innovatetech /etc/nginx/sites-enabled/
sudo rm /etc/nginx/sites-enabled/default

# Comprobar configuración y reiniciar Nginx
sudo nginx -t
sudo systemctl restart nginx
```

Acceso tras la configuración:
```
http://100.49.223.120
```

---

## Servicio SFTP

```bash
# Habilitar SSH
sudo systemctl enable ssh && sudo systemctl start ssh

# Instalar paquetes para unirse al dominio LDAP
sudo apt install sssd sssd-ldap ldap-utils -y
```

Configurar `/etc/sssd/sssd.conf` para validar usuarios de LDAP mediante SFTP:

```bash
# Asignar permisos al archivo y reiniciar sssd
sudo chmod 600 /etc/sssd/sssd.conf
sudo systemctl restart sssd

# Comprobar que se muestra un usuario del dominio en el servidor local
id <usuario_ldap>
```

Modificar `/etc/ssh/sshd_config` para que:
- `admin-innovate` tenga acceso SSH completo al servidor
- Los usuarios autenticados mediante LDAP solo puedan usar comandos **SFTP** (sin acceso SSH completo)

```bash
# Reiniciar el servicio SSH
sudo systemctl restart ssh

# Crear automáticamente el directorio personal de usuarios LDAP en su primer inicio de sesión
sudo pam-auth-update --enable mkhomedir
```
