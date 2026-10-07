# 🛡️ SOC Analyst Training & Lab Notebook

Bienvenido a mi repositorio de entrenamiento para **Analista SOC**. Aquí documento mis proyectos prácticos, análisis de tráfico de red, operaciones SIEM e investigación de amenazas.

📌 **Cuaderno de Bitácora En Vivo (Notion):** [Haz clic aquí para ver mis capturas y reportes detallados](https://spicy-clownfish-847.notion.site/SOC-Analyst-Lab-Notebook-3ef29add16b480cf915ec90482ca371d?source=copy_link)

---

## 🛠️ Stack Tecnológico & Herramientas
* **Sistemas Operativos:** Ubuntu Linux, Ubuntu Server, VirtualBox, SSH.
* **Plataformas de aprendizaje:** Cisco Networking Academy.
* **Redes & Análisis:** Wireshark, CLI Net-Tools.
* **Seguridad & Laboratorios:** OverTheWire, Wazuh, Splunk, MITRE ATT&CK.
* **Documentación & OPSEC:** GitHub, Notion.

---

## 📚 Fase 1: Comandos Esenciales de Linux & Redes (Cheatsheet)

### Diagnóstico de Red (Capa 3 & 7)
| Comando | Descripción | Caso de Uso en SOC |
| :--- | :--- | :--- |
| `ip a` | Muestra interfaces y direcciones IP | Identificar IP local e interfaces de red activas |
| `ping -c 4 <IP>` | Envía paquetes ICMP Echo Request | Verificar conectividad básica con un host |
| `curl -I <URL>` | Trae solo las cabeceras HTTP/S | Inspeccionar respuestas del servidor web sin descargar el cuerpo |

### Navegación y Manipulación de Archivos
| Comando | Descripción | Caso de Uso en SOC |
| :--- | :--- | :--- |
| `ls -la` | Lista todos los archivos, incluidos ocultos (`.`) | Detectar malware o scripts ocultos en directorios |
| `cat ./-` | Lee un archivo cuyo nombre es un guion | Evitar la interpretación del guion como bandera de comando |
| `cat "file name"`| Lee un archivo con espacios en el nombre | Analizar logs o archivos con nombres no estandarizados |

---

### Análisis de Logs y Búsqueda Forense
| Comando | Descripción | Caso de Uso en SOC |
| :--- | :--- | :--- |
| `file <archivo>` | Determina el tipo real de archivo (*magic bytes*) | Detectar artefactos maliciosos camuflados con extensiones falsas |
| `find <ruta> -size <bytes>` | Búsqueda por atributos de sistema (tamaño, permisos, usuario) | Localizar archivos sospechosos o modificados en el servidor |
| `grep "patrón" <archivo>` | Filtra líneas de texto que coincidan con un término | Identificar IoCs, IPs maliciosas o eventos clave dentro de logs |
| `2>/dev/null` | Redirige la salida de error estándar (STDERR) | Silenciar errores de "permiso denegado" para reducir ruido |

---

*Prototipo de Portafolio en construcción continua.*
