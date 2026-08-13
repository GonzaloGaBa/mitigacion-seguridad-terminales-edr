# Caso de Estudio: Mitigación de Vulnerabilidades en Terminales y Selección de Solución EDR/EPP

![Category](https://img.shields.io/badge/Category-Cybersecurity_%26_SOC-blue?style=for-the-badge)
![Focus](https://img.shields.io/badge/Focus-Endpoint_Hardening_%7C_Risk_Assessment-brightgreen?style=for-the-badge)
![Level](https://img.shields.io/badge/Level-Junior_SOC_/_Security_Analyst-orange?style=for-the-badge)

## 📋 Resumen Ejecutivo

Este caso de estudio aborda la evaluación de riesgos de seguridad y el diseño de estrategias de mitigación para dos escenarios empresariales distintos:

1. **Entorno Industrial / SCADA:** Una empresa de fabricación que requiere cumplir con estándares estrictos de ciberseguridad para adjudicarse un contrato comercial. Presenta vulnerabilidades críticas en sus terminales, incluyendo sistemas operativos obsoletos (Windows XP), uso descontrolado de medios USB, dispositivos BYOD no gestionados y falta de protección endpoint centralizada.
2. **Startup Tecnológica en Crecimiento:** Una empresa en fase de escalamiento acelerado que requiere seleccionar una solución integral de protección de terminales (**EPP/EDR**) basada en la nube, optimizada para despliegue rápido, alta visibilidad y costo-efectividad.

El objetivo de este proyecto es aplicar el principio de **Defensa en Profundidad (Defense in Depth)**, diseñar controles de compensación alineados con marcos internacionales (NIST SP 800-53 / CIS Controls) y justificar la selección de tecnología EDR Enterprise.

---

## 🎯 Objetivos Técnicos

* Evaluar la superficie de ataque y el impacto de vulnerabilidades en terminales críticas (OT/IT).
* Proponer procedimientos de mitigación técnica y políticas de endurecimiento (**Endpoint Hardening**).
* Implementar mecanismos de segmentación y control de acceso a la red (**NAC / BYOD Isolation**).
* Diseñar estrategias de seguridad web y filtrado de dominio (**DNS Security / SWG**).
* Evaluar y seleccionar una plataforma **EDR/EPP Cloud-Native** adecuada para empresas en crecimiento.

---

## 🏗️ Caso de Estudio 1: Evaluación y Mitigación de Vulnerabilidades en Planta Industrial (SCADA)

### Contexto del Riesgo
En los entornos de tecnología operativa (**OT / SCADA**), la disponibilidad y continuidad del negocio son prioritarias. A menudo, el software industrial crítico requiere ejecutarse sobre sistemas operativos legados sin soporte oficial de parches. Sin embargo, exponer estos sistemas a vectores de ataque físicos o de red incrementa exponencialmente el riesgo de incidentes graves (ej. ransomware industrial, exfiltración de datos, ataques a la cadena de suministro).

### Matriz de Evaluación de Riesgos y Mitigación Técnica

| Vector / Vulnerabilidad Identificada | Nivel de Riesgo | Impacto Operativo / Amenaza | Controles de Mitigación Recomendados (Hardening) |
| :--- | :---: | :--- | :--- |
| **Sistemas Operativos Obsoletos (Windows XP en SCADA)** | **Crítico** | Ejecución remota de código (RCE), exploits sin parchear (*Zero-Day*), compromiso total del sistema industrial. | **Segmentación de Red y Aislamiento OT:** Ubicar los sistemas SCADA en una VLAN/zona industrial dedicada siguiendo el modelo Purdue. Aplicar reglas de Firewall/ACLs que bloqueen el tráfico entrante/saliente no esencial y deshabiliten el acceso a Internet. Aplicar microsegmentación e inspección profunda de paquetes (DPI) como control compensatorio. |
| **Uso no controlado de medios USB en equipos críticos** | **Alto** | Introducción de malware (BadUSB, autorun, Stuxnet) y exfiltración de información confidencial. | **Hardening de Endpoints y GPO:** Deshabilitar puertos USB a nivel BIOS y mediante Políticas de Grupo (GPO). En caso de requerir transferencia de datos, implementar una **Estación de Desinfección USB (Kiosk)** y exigir el uso de pendrives corporativos cifrados con listas blancas de Hardware ID. |
| **Acceso de dispositivos personales no gestionados (BYOD)** | **Alto** | Movimiento lateral de malware desde dispositivos de usuarios hacia la red de producción/servidores. | **Control de Acceso a la Red (NAC):** Desplegar una solución NAC (ej. Cisco ISE) para autenticación 802.1X y validación de la postura de seguridad. Aislar el tráfico BYOD en una **VLAN de Invitados** independiente con acceso únicamente a Internet y sin enrutamiento a la red OT/IT corporativa. |
| **Navegación web libre hacia sitios maliciosos** | **Medio / Alto** | Phishing, descarga de malware de segunda etapa (*Drive-by download*) y conexiones Command & Control (C2). | **Filtrado Web / Secure Web Gateway:** Implementar protección a nivel DNS/Web (ej. Cisco Umbrella) para bloquear dominios maliciosos, categorías de riesgo y comunicaciones C2. Configurar el principio de **mínimo privilegio** restringiendo la navegación únicamente a sitios autorizados (*Whitelisting*). |
| **Antivirus inconsistente y firmas desactualizadas** | **Alto** | Incapacidad para detectar amenazas modernas o ataques basados en código polimórfico/sin archivos (*Fileless*). | **Gestión Centralizada con EPP/EDR:** Reemplazar las instalaciones locales e individuales por una consola unificada de protección de terminales (EPP/EDR) administrada centralmente. Garantizar telemetría constante, actualizaciones automáticas de firmas y alertas en tiempo real hacia el SOC. |

---

## 🚀 Caso de Estudio 2: Selección de Solución EDR/EPP para Startup en Crecimiento

### Contexto del Negocio
Una startup tecnológica requiere proteger sus terminales de trabajo (desarrolladores, administración, ventas) tras recibir financiamiento. La empresa opera en un modelo híbrido/remoto, planea duplicar su personal en corto tiempo y no cuenta con infraestructura física dedicada para servidores de seguridad (*On-Premises*).

### Ficha Técnica de la Solución Seleccionada

**Producto Recomendado:** `Cisco Secure Endpoint` *(o CrowdStrike Falcon Platform)*

| Criterio / Característica | Especificación / Justificación Técnica |
| :--- | :--- |
| **Modelo de Despliegue** | **100% Cloud-Native (SaaS):** No requiere inversión en servidores locales ni mantenimiento de infraestructura. Permite la instalación remota y automática del agente mediante herramientas MDM/RMM. |
| **Capacidades de Prevención (EPP)** | Antivirus de Próxima Generación (NGAV), análisis heurístico, protección en tiempo real contra Ransomware, bloqueo de exploits y prevención de ejecución de scripts no autorizados. |
| **Detección y Respuesta (EDR)** | Monitoreo continuo de procesos e hilos en memoria, análisis de comportamiento (*Behavioral Analysis*), retrospectiva de archivos (*File Retrospection*) para detectar amenazas latentes y aislamiento remoto del host comprometido con un solo clic. |
| **Inteligencia de Amenazas** | Integración nativa con **Cisco Talos**, garantizando la actualización automática de indicadores de compromiso (IoCs) e inteligencia global en tiempo real. |
| **Escalabilidad y Costos** | Esquema de licenciamiento por suscripción (*Pay-as-you-grow*). Permite escalar de manera transparente desde decenas hasta miles de endpoints sin degradación del servicio. |
| **Compatibilidad Multiplataforma** | Soporte multiplataforma completo: Windows, macOS, Linux, iOS y Android. |
| **Integración SOC / XDR** | Capacidad de enviar telemetría detallada a través de APIs REST y Syslog hacia un SIEM/XDR para correlación de eventos y automatización de respuestas (SOAR). |

---

## 🔍 Verificaciones y Buenas Prácticas Aplicadas

1. **Principio de Mínimo Privilegio (Least Privilege):** Restricción de acceso administrativo en las terminales y limitación de puertos físicos y de red a los estrictamente necesarios.
2. **Defensa en Profundidad (Defense in Depth):** Implementación de seguridad en múltiples niveles: Perímetro → Red/VLANs → Endpoint → Políticas de Usuario.
3. **Controles Compensatorios en OT:** Ante la imposibilidad de actualizar el SO industrial, se reforzaron la segmentación de red y el monitoreo pasivo de tráfico.

---

## 💡 Conceptos Clave Aprendidos

* **Diferencia entre Antivirus Tradicional y EDR:** El antivirus tradicional depende de firmas estáticas (hashes de malware conocido), mientras que el EDR analiza comportamientos anómalos en memoria/procesos, detectando ataques de día cero (*Zero-Day*) y amenazas *fileless*.
* **Modelo Purdue para Redes Industriales:** Principio de diseño que separa la red corporativa (IT) de la red de control de proceso (OT) mediante capas de seguridad y zonas DMZ industriales.
* **Network Access Control (NAC):** Mecanismo para auditar y autorizar dispositivos antes de otorgarles acceso a la red corporativa.

---

## 📌 Conclusión

La seguridad de las terminales es la última línea de defensa contra intrusiones en la red corporativa o industrial. La implementación de medidas de hardening (desactivación de USB, segmentación de red, filtrado DNS) junto con el despliegue de soluciones **EDR administradas en la nube** proporciona la visibilidad, prevención y capacidad de respuesta requeridas tanto para proteger infraestructuras críticas (SCADA) como para habilitar el crecimiento seguro de organizaciones modernas.

---
