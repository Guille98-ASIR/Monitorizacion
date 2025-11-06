# Monitorización de Servidores

![Status](https://img.shields.io/badge/Estado-Activo-success?style=for-the-badge)
![Dificultad](https://img.shields.io/badge/Dificultad-Básico-blue?style=for-the-badge)
![Tema](https://img.shields.io/badge/Tema-Monitorización-orange?style=for-the-badge)

## 🔍 ¿Qué es monitorizar?

La **monitorización de servidores** es el proceso continuo de supervisar y recopilar datos sobre el funcionamiento de los sistemas informáticos, tanto a nivel de *hardware* (CPU, memoria, disco, red) como de *software* (procesos, servicios, aplicaciones). Este seguimiento permite detectar problemas, optimizar el rendimiento y garantizar la disponibilidad de los servicios.

---

## 🛠️ Herramientas para Monitorizar Procesos

### 1️⃣ Comando `ps`

![Linux](https://img.shields.io/badge/Linux-FCC624?style=flat&logo=linux&logoColor=black)
![Shell](https://img.shields.io/badge/Shell-4EAA25?style=flat&logo=gnu-bash&logoColor=white)

El comando `ps` muestra información sobre los procesos activos en el sistema. Es una herramienta fundamental para la administración de sistemas Linux.

#### 📋 `ps -au`
Proporciona información detallada de todos los procesos del usuario actual, incluyendo el uso de CPU y memoria.

![Comando ps -au](/ud1/img/ps1.png)

#### 📊 `ps aux`
Muestra información completa de **todos los procesos del sistema**, independientemente del usuario que los ejecute. Esta es una de las variantes más utilizadas.

![Comando ps aux](/ud1/img/ps2.png)

#### 👤 `ps -u <usuario>`
Filtra y muestra únicamente los procesos lanzados por un usuario específico, útil para auditorías o depuración.

![Comando ps -u](/ud1/img/ps3.png)

---

### 2️⃣ Comando `top`

![Monitoring](https://img.shields.io/badge/Monitorización-Real%20Time-green?style=flat&logo=grafana)

El comando `top` ofrece una **vista dinámica y en tiempo real** de los procesos del sistema, actualizándose automáticamente cada pocos segundos.

#### ⚙️ Características principales:
- **🔄 Ordenación interactiva**: Puedes ordenar los procesos presionando diferentes teclas:
  - `M`: Ordenar por uso de **memoria** (de mayor a menor)
  - `P`: Ordenar por uso de **CPU**
  - `T`: Ordenar por **tiempo de ejecución**
- **⏱️ Actualización automática**: La pantalla se refresca constantemente mostrando el estado actual del sistema

![Vista principal de top](/ud1/img/top1.png)

#### 💾 Exportar información de `top`

Es posible redirigir la salida de `top` a un archivo de texto para su posterior análisis o para compartir la información con otros administradores:

```bash
top -b -n 1 > top_output.txt
```

![Redirigiendo top a archivo](/ud1/img/top2.png)

El contenido del archivo puede visualizarse con cualquier editor o con el comando `cat`:

![Contenido del archivo top](/ud1/img/top3.png)

---

### 3️⃣ Comando `htop`

![Interactive](https://img.shields.io/badge/Interfaz-Interactiva-blueviolet?style=flat&logo=windowsterminal)
![Recommended](https://img.shields.io/badge/★-Recomendado-yellow?style=flat)

`htop` es una **versión mejorada e interactiva** de `top`, con una interfaz más visual y amigable. Incluye:

- 📊 Gráficos de barras para CPU y memoria
- 🎨 Código de colores para facilitar la lectura
- ⌨️ Navegación con teclas de dirección
- ❓ Menús de ayuda integrados (F1-F10)
- 🔍 Búsqueda y filtrado de procesos
- ⚡ Gestión de procesos directa (kill, nice, renice)

![Interfaz de htop](/ud1/img/htop.png)

> **💡 Nota**: `htop` no viene instalado por defecto en todas las distribuciones. Puedes instalarlo con: 
> - `sudo apt install htop` (Debian/Ubuntu)
> - `sudo yum install htop` (RHEL/CentOS)

---

## 📝 Ejercicio Práctico

![Exercise](https://img.shields.io/badge/Tipo-Ejercicio-red?style=flat&logo=ansible)

**🎯 Objetivo**: Crear un comando que muestre únicamente los procesos que más CPU consumen, filtrando las columnas relevantes.

**✅ Solución**: El siguiente comando muestra los campos `USER`, `COMMAND`, `PID` y `%CPU` ordenados por consumo de CPU:

```bash
ps aux --sort=-%cpu | awk '{print $1, $11, $2, $3}' | head -n 11
```

![Resultado del ejercicio](/ud1/img/ejercicioprocesos.png)

💡 Este tipo de consultas personalizadas son muy útiles para diagnósticos rápidos y scripts de monitorización automatizada.

---

## 🧭 Navegación

[![Siguiente](https://img.shields.io/badge/→_Siguiente_Tema-Unidad_2-blue?style=for-the-badge)](/ud2/ud2.md)

[![Documentos](https://img.shields.io/badge/📄_Documentos-Referencia-green?style=for-the-badge)](/ud1/documentos)
[![Imágenes](https://img.shields.io/badge/🖼️_Imágenes-Recursos-orange?style=for-the-badge)](/ud1/img)
[![Inicio](https://img.shields.io/badge/🏠_Volver-README-purple?style=for-the-badge)](/README.md)
