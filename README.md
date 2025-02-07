# 📌 Guía de Uso de Proxmark3 (AliExpress) en Windows

## 📜 Índice
1. [Requisitos Previos](#requisitos-previos)
2. [Conexión del Proxmark3](#conexión-del-proxmark3)
3. [Descarga y Configuración de ProxSpace](#descarga-y-configuración-de-proxspace)
4. [Instalación del Firmware](#instalación-del-firmware)
5. [Flasheo del Proxmark3](#flasheo-del-proxmark3)
6. [Uso del Cliente Proxmark3](#uso-del-cliente-proxmark3)
7. [Comandos Básicos](#comandos-básicos)
8. [Ataques y Clonación de Tarjetas](#ataques-y-clonación-de-tarjetas)
9. [Conclusión](#conclusión)

---

## 🔹 1. Requisitos Previos
Antes de comenzar, asegúrate de tener lo siguiente:

- ✅ Windows 10 o superior (64 bits)
- ✅ Un puerto USB disponible
- ✅ Proxmark3 (versión AliExpress)
- ✅ Conexión a internet para descargar software

---

## 🔹 2. Conexión del Proxmark3
1. Conecta el **Proxmark3** a un puerto USB del ordenador.
2. Abre el **Administrador de dispositivos** y busca el puerto COM asignado (ejemplo: `COM5`).

![Detección del COM](ruta-a-imagen)

---

## 🔹 3. Descarga y Configuración de ProxSpace
1. Descarga la última versión de **ProxSpace** desde:
   - [ProxSpace en GitHub](https://github.com/Gator96100/ProxSpace/releases)
2. Extrae el contenido del archivo en `C:\` (debe quedar como `C:\ProxSpace`).

![Archivos extraídos](ruta-a-imagen)

3. Abre `runme64.bat` desde la carpeta `C:\ProxSpace`.

---

## 🔹 4. Instalación del Firmware
1. En la terminal de ProxSpace, ejecuta:
   ```sh
   git clone https://github.com/RfidResearchGroup/proxmark3.git
   ```

![Clonación del repositorio](ruta-a-imagen)

2. Accede a la carpeta:
   ```sh
   cd proxmark3
   ```

![Acceso a la carpeta proxmark3](ruta-a-imagen)

3. Copia el archivo de configuración de la plataforma:
   ```sh
   cp Makefile.platform.sample Makefile.platform
   ```
4. Edita `Makefile.platform`:
   ```sh
   notepad Makefile.platform
   ```
   - Descomenta `PLATFORM=PM3GENERIC`
   - Comenta `PLATFORM=PM3RDV4`

![Edición de Makefile.platform](ruta-a-imagen)

5. Compila el firmware:
   ```sh
   make clean && make -j8 all
   ```

![Compilación del firmware](ruta-a-imagen)

---

## 🔹 5. Flasheo del Proxmark3
1. Flashear el **Bootrom**:
   ```sh
   ./pm3-flash-bootrom
   ```

![Flasheo Bootrom](ruta-a-imagen)

2. Flashear el **Firmware completo**:
   ```sh
   ./pm3-flash-fullimage -p COM5
   ```

![Flasheo Fullimage](ruta-a-imagen)

---

## 🔹 6. Uso del Cliente Proxmark3
1. Inicia el cliente Proxmark3:
   ```sh
   ./pm3
   ```

![Inicio del cliente Proxmark3](ruta-a-imagen)

2. Para ver los comandos disponibles:
   ```sh
   help
   ```

![Lista de comandos](ruta-a-imagen)

---

## 🔹 7. Comandos Básicos
| Comando | Descripción |
|---------|------------|
| `lf` | Modo baja frecuencia |
| `hf` | Modo alta frecuencia |
| `auto` | Escaneo automático de tarjeta |
| `hf mf autopwn` | Ataque a tarjetas Mifare 1K |
| `hf mf cload -f <archivo>` | Carga de datos a una nueva tarjeta |

---

## 🔹 8. Ataques y Clonación de Tarjetas
### 🔸 Escaneo de tarjeta
Para detectar el tipo de tarjeta presente en el lector:
```sh
auto
```

![Escaneo de tarjeta](ruta-a-imagen)

### 🔸 Ataque y obtención de claves
Para atacar una tarjeta Mifare 1K sin protecciones avanzadas:
```sh
hf mf autopwn
```

![Ataque hf mf autopwn](ruta-a-imagen)

### 🔸 Clonación de tarjeta
1. Copiar los datos obtenidos:
   ```sh
   hf mf cload -f <archivo-dump>
   ```
2. Colocar la nueva tarjeta en el lector y ejecutar el comando.

![Clonación de tarjeta](ruta-a-imagen)

---

## 🔹 9. Conclusión

¡Ahora tienes tu **Proxmark3** configurado y listo para pruebas! 🎉

Para más información, revisa la documentación oficial:
- [Wiki de Proxmark3](https://github.com/RfidResearchGroup/proxmark3/wiki)
