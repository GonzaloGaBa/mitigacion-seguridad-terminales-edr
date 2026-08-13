# Caso de Estudio: Mitigación de Vulnerabilidades en Terminales y Selección de Solución EDR/EPP

![Category](https://img.shields.io/badge/Category-Cybersecurity_%26_SOC-blue?style=for-the-badge)
![Focus](https://img.shields.io/badge/Focus-Endpoint_Hardening_%7C_Risk_Assessment-brightgreen?style=for-the-badge)
![Level](https://img.shields.io/badge/Level-Junior_SOC_/_Security_Analyst-orange?style=for-the-badge)

# 🛡️ Caso de Estudio: Mitigación de Vulnerabilidades en Terminales y Selección de Soluciones EDR/EPP

## 📌 Descripción del Proyecto
Este laboratorio presenta una evaluación técnica de riesgos y diseño de mitigaciones para terminales en entornos corporativos e industriales (SCADA/OT), junto con la ficha técnica para la selección de una plataforma EDR (Endpoint Detection and Response) basada en la nube.

---

## 🎯 Objetivos Técnicos
- Evaluar la superficie de ataque e impacto de vulnerabilidades en terminales críticas (OT/IT).
- Definir controles de hardening, segmentación (Modelo Purdue) y control de acceso a la red (NAC).
- Seleccionar e integrar una solución EDR/EPP orientada a la visibilidad y respuesta de un SOC.

---

## 📋 Caso de Estudio 1: Matriz de Riesgos y Mitigación SCADA / OT

En los entornos industriales, la continuidad operativa es prioritaria y suele convivir con sistemas heredados. A continuación se detallan los vectores de ataque identificados y sus controles de compensación:

| Vulnerabilidad / Publicación | Recomendación Técnica Profesional (Mitigación) |
| :--- | :--- |
| **Versiones obsoletas del sistema operativo (Windows XP / SCADA)** | **Aislamiento de Red y Segmentación:** Aislar los sistemas SCADA en una VLAN/zona industrial dedicada (Modelo Purdue) sin acceso directo a Internet. Implementar reglas estrictas de Firewall/ACLs. Si no se puede actualizar el SO por incompatibilidad, aplicar compensación de controles con microsegmentación e inspección profunda de paquetes (DPI). |
| **Sistemas críticos permiten el uso de medios USB** | **Hardening de Endpoints y Políticas de Grupo (GPO):** Deshabilitar puertos USB a nivel BIOS/Sistema Operativo mediante GPO. Si se requiere intercambio de datos, implementar un "USB Kiosk/Sanitization Station" (estación de desinfección) y usar únicamente pendrives cifrados corporativos con listas blancas de IDs de hardware. |
| **Uso de dispositivos de computación personal en la red (BYOD)** | **Control de Acceso a la Red (NAC) y Red de Invitados:** Implementar una solución NAC (ej. Cisco ISE) para autenticar y evaluar la postura del dispositivo. Separar el tráfico de dispositivos personales en una **VLAN de Invitados/BYOD** aislada con acceso restringido solo a Internet y sin visibilidad hacia la red de fabricación o servidores. |
| **Navegación libre por la WWW (Sitios dañinos)** | **Filtrado Web y DNS Security:** Desplegar una solución de seguridad web/DNS (ej. Cisco Umbrella, Secure Web Gateway) para bloquear categorías de riesgo, URLs maliciosas y conexiones C2 (Command & Control). Configurar la regla de "mínimo privilegio" para permitir navegación únicamente a sitios estrictamente necesarios para la operación. |
| **Problemas de antivirus (Inconsistente / Desactualizado)** | **Gestión Centralizada con EPP/EDR:** Reemplazar consolas antivirus locales e individuales por una plataforma de protección de terminales centralizada en la nube o servidor local (EPP/EDR). Configurar actualizaciones automáticas de definiciones/telemetría y alertas en tiempo real hacia el equipo SOC. |

---

## 🚀 Caso de Estudio 2: Ficha Técnica de Selección EDR / EPP

Evaluación técnica de una solución de protección de terminales en la nube (ej. **Cisco Secure Endpoint** / **CrowdStrike Falcon**) para una organización en rápido crecimiento:

| Característica / Requisito | Valor / Justificación Técnica |
| :--- | :--- |
| **Nombre del Producto / Solución** | **Cisco Secure Endpoint** (anteriormente Cisco AMP for Endpoints) / **CrowdStrike Falcon Platform**. |
| **Arquitectura de Despliegue** | **100% Cloud-Managed (SaaS):** No requiere infraestructura on-premise (servidores dedicados) en la startup. Permite desplegar agentes de forma remota y rápida a medida que la empresa contrata nuevo personal. |
| **Capacidades de Prevención (EPP)** | Antivirus de próxima generación (NGAV), análisis heurístico, protección contra ransomware, listas de bloqueo/permitidos y prevención de exploits en tiempo real. |
| **Capacidades de Detección y Respuesta (EDR)** | Monitoreo continuo de procesos, análisis del comportamiento de archivos (Behavioral Analysis), retrospectiva de archivos (File Retrospection) para detectar amenazas que cambiaron de reputación, y aislamiento remoto del host comprometido. |
| **Inteligencia de Amenazas (Threat Intelligence)** | Integración nativa con **Cisco Talos** (o CrowdStrike Falcon Intelligence), lo que permite actualizar firmas y patrones de ataque automáticamente a nivel global en segundos. |
| **Escalabilidad y Flexibilidad** | Licenciamiento basado en suscripción por agente/usuario. Ideal para startups: se paga por lo que se usa y escala sin fricción de 10 a 1,000+ endpoints. |
| **Compatibilidad Multiplataforma** | Soporte completo para Windows, macOS, Linux, iOS y Android (cubriendo equipos corporativos y móviles). |
| **Integración SOC / XDR** | Capacidad de enviar telemetría mediante APIs/Syslog hacia soluciones SIEM / XDR para correlación de eventos y automatización de respuestas (SOAR). |

---

## 💡 Conceptos Clave Aprendidos
* **Controles Compensatorios:** Estrategias implementadas cuando un control de seguridad primario (como actualizar un SO) no es técnicamente viable.
* **Modelo Purdue:** Estructura de referencia para segmentar redes industriales y proteger sistemas SCADA de la red corporativa/Internet.
* **Antivirus Tradicional vs. EDR:** Cambio de paradigma de detección basada en firmas estáticas hacia el análisis continuo del comportamiento del sistema.

---
- GitHub: [@GonzaloGaBa](https://github.com/GonzaloGaBa)
---
