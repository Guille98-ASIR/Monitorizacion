# Memoria, Espacio y Rendimiento del Disco

![Status](https://img.shields.io/badge/Estado-Activo-success?style=for-the-badge)
![Dificultad](https://img.shields.io/badge/Dificultad-Intermedio-yellow?style=for-the-badge)
![Tema](https://img.shields.io/badge/Tema-Recursos_del_Sistema-orange?style=for-the-badge)

## 📊 Introducción

La monitorización de **memoria**, **espacio en disco** y **rendimiento de E/S** es fundamental para mantener un sistema saludable y detectar cuellos de botella que puedan afectar el rendimiento general del servidor.

---

## 🛠️ Herramientas de Monitorización




### 2️⃣ Comando `free`

![Memory](https://img.shields.io/badge/Monitoriza-Memoria_RAM-blue?style=flat&logo=memory)

Muestra información sobre el uso de **memoria RAM** y **swap** del sistema.

#### 📊 Uso básico

![free](/ud2/img/free.png)


**Parámetros útiles:**
- `-h`: Muestra los valores en formato **humano** (MB, GB)
- `-m`: Muestra los valores en **megabytes**
- `-g`: Muestra los valores en **gigabytes**
- `-s N`: Actualiza cada **N segundos** (ej: `free -h -s 2`)

#### 📋 Interpretación de resultados

```
              total        used        free      shared  buff/cache   available
Mem:           15Gi       8.2Gi       1.1Gi       428Mi       6.1Gi       6.5Gi
Swap:         2.0Gi          0B       2.0Gi
```

**Columnas importantes:**
- **total**: Memoria total instalada
- **used**: Memoria actualmente en uso
- **free**: Memoria completamente libre
- **buff/cache**: Memoria usada para cachés (se libera si es necesaria)
- **available**: Memoria realmente disponible para nuevas aplicaciones
- **Swap**: Memoria de intercambio en disco

---

### 3️⃣ Comando `df`

![Disk](https://img.shields.io/badge/Monitoriza-Espacio_en_Disco-orange?style=flat&logo=harddisk)

Muestra el **espacio disponible y utilizado** en los sistemas de archivos montados.

#### 💾 Uso básico

![df](/ud2/img/df.png)

**Parámetros útiles:**
- `-h`: Formato **legible** para humanos (KB, MB, GB)
- `-T`: Muestra el **tipo de sistema de archivos** (ext4, xfs, etc.)
- `-i`: Muestra información sobre **inodos** en lugar de bloques
- `--total`: Añade una línea con el **total** de todos los sistemas de archivos

#### 📊 Ejemplo de salida

```bash
df -hT
```

```
Sistema de archivos Tipo     Tamaño Usados  Disp Uso% Montado en
/dev/sda1           ext4       50G    35G   12G  75% /
/dev/sdb1           xfs       200G   150G   50G  75% /data
tmpfs               tmpfs     7.8G   1.2M  7.8G   1% /run
```

**💡 Tip**: Si un sistema de archivos alcanza el **100%**, puede causar errores en aplicaciones y servicios.

---

### 4️⃣ Comando `du`

![Disk Usage](https://img.shields.io/badge/Analiza-Uso_de_Disco-purple?style=flat&logo=files)

Analiza el **uso de espacio en disco** por directorios y archivos.

#### 📁 Uso básico

![dh](/ud2/img/du.png)

**Parámetros útiles:**
- `-h`: Formato **legible** (KB, MB, GB)
- `-s`: Muestra solo el **resumen total** del directorio
- `-a`: Incluye **archivos individuales**, no solo directorios
- `--max-depth=N`: Limita la profundidad de exploración a **N niveles**
- `-c`: Muestra un **total general** al final

#### 🔍 Ejemplos prácticos

**Encontrar los 10 directorios más grandes:**
```bash
du -h /home | sort -rh | head -10
```

**Ver uso de disco del directorio actual (1 nivel):**
```bash
du -h --max-depth=1 | sort -rh
```

**Analizar uso de disco incluyendo archivos ocultos:**
```bash
du -sh .[!.]* * | sort -rh
```

---

### 5️⃣ Comando `iostat`

![I/O](https://img.shields.io/badge/Monitoriza-E/S_de_Disco-red?style=flat&logo=databricks)
![Performance](https://img.shields.io/badge/Tipo-Rendimiento-yellow?style=flat)

Muestra estadísticas de **entrada/salida (I/O)** de los dispositivos de almacenamiento y uso de CPU.

#### 📈 Uso básico

![iostat](/ud2/img/iostat.png)

**Parámetros útiles:**
- `-x`: Muestra estadísticas **extendidas** (más detalladas)
- `-h`: Formato **legible** para humanos
- `-c`: Muestra solo estadísticas de **CPU**
- `-d`: Muestra solo estadísticas de **disco**
- `N`: Actualiza cada **N segundos** (ej: `iostat 2` actualiza cada 2 segundos)
- `-p`: Muestra estadísticas por **partición**

#### 📊 Interpretación de métricas clave

```bash
iostat -x 1
```

**Métricas importantes:**
- **%util**: Porcentaje de tiempo que el disco estuvo ocupado (>80% indica saturación)
- **await**: Tiempo promedio de espera de las operaciones I/O (en ms)
- **r/s**: Lecturas por segundo
- **w/s**: Escrituras por segundo
- **rkB/s**: Kilobytes leídos por segundo
- **wkB/s**: Kilobytes escritos por segundo

**⚠️ Señales de problemas:**
- `%util` cercano al 100%
- `await` muy alto (>20ms para SSD, >10ms para discos rápidos)
- Valores de `r/s` o `w/s` anormalmente altos

#### 💡 Ejemplo de análisis

```bash
iostat -xh 2 5
```
Este comando muestra estadísticas extendidas en formato legible, actualizadas cada 2 segundos, durante 5 iteraciones.

---

## 🎯 Ejercicio Práctico

![Exercise](https://img.shields.io/badge/Tipo-Ejercicio-success?style=flat&logo=checkmarx)

### Objetivo: Monitorización completa del sistema

1. **🔴 Genera carga en el sistema:**
   ```bash
   for i in {1..2}; do yes >/dev/null & done
   ```

2. **📊 Monitoriza con múltiples herramientas:**
   ```bash
   # Terminal 1: Monitoriza procesos
   atop
   
   # Terminal 2: Observa memoria
   watch -n 1 free -h
   
   # Terminal 3: Verifica I/O de disco
   iostat -x 2
   ```

3. **🧹 Limpia los procesos de prueba:**
   ```bash
   killall yes
   ```

4. **📈 Analiza uso de disco:**
   ```bash
   # Espacio en sistemas de archivos
   df -hT
   
   # Directorios más grandes en /var
   du -h --max-depth=1 /var | sort -rh | head -10
   ```

---

## 📚 Resumen de Comandos

| Comando | Función | Ejemplo |
|---------|---------|---------|
| `atop` | Monitorización avanzada integral | `atop` |
| `free` | Uso de memoria RAM y swap | `free -h` |
| `df` | Espacio en discos/particiones | `df -hT` |
| `du` | Uso de disco por directorio | `du -sh /var/*` |
| `iostat` | Estadísticas de I/O y CPU | `iostat -x 2` |

---

## 🧭 Navegación

[![Anterior](https://img.shields.io/badge/←_Tema_Anterior-Unidad_1-blue?style=for-the-badge)](/ud1/ud1.md)

[![Siguiente](https://img.shields.io/badge/→_Siguiente_Tema-Unidad_3-blue?style=for-the-badge)](/ud3/ud3.md)

[![Documentos](https://img.shields.io/badge/📄_Documentos-Referencia-green?style=for-the-badge)](/ud2/documentos)

[![Imágenes](https://img.shields.io/badge/🖼️_Imágenes-Recursos-orange?style=for-the-badge)](/ud2/img)

[![Inicio](https://img.shields.io/badge/🏠_Volver-README-purple?style=for-the-badge)](/README.md)
