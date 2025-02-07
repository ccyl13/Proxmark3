# 📌 Guía de Uso de Proxmark3 (AliExpress) en Windows

![Proxmark3](https://github.com/ccyl13/Proxmark3/blob/main/proxmark3.jpeg?raw=true)

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

![Detección del COM](https://github.com/ccyl13/Proxmark3/blob/main/deteccion%20del%20com.png?raw=true)

---

## 🔹 3. Descarga y Configuración de ProxSpace
1. Descarga la última versión de **ProxSpace** desde:
   - [ProxSpace en GitHub](https://github.com/Gator96100/ProxSpace/releases)
2. Extrae el contenido del archivo en `C:\` (debe quedar como `C:\ProxSpace`).

![Archivos extraídos](https://github.com/ccyl13/Proxmark3/blob/main/extraer%20carpeta.png?raw=true)

3. Abre `runme64.bat` desde la carpeta `C:\ProxSpace`.

---

## 🔹 4. Instalación del Firmware
1. En la terminal de ProxSpace, ejecuta:
   ```sh
   git clone https://github.com/RfidResearchGroup/proxmark3.git
   ```

![Clonación del repositorio](https://github.com/ccyl13/Proxmark3/blob/main/comando%201.png?raw=true)

2. Accede a la carpeta:
   ```sh
   cd proxmark3
   ```

![Acceso y configuración](https://github.com/ccyl13/Proxmark3/blob/main/comando%202.png?raw=true)

3. Copia el archivo de configuración de la plataforma:
   ```sh
   cp Makefile.platform.sample Makefile.platform
   ```
4. Edita `Makefile.platform`:
   ```sh
   notepad Makefile.platform
   ```
   - **Debes cambiar:**
     - **Comentar** `PLATFORM=PM3RDV4`
     - **Descomentar** `PLATFORM=PM3GENERIC`

![Antes del cambio de plataforma](https://github.com/ccyl13/Proxmark3/blob/main/1.png?raw=true)

![Después del cambio de plataforma](https://github.com/ccyl13/Proxmark3/blob/main/2.png?raw=true)

5. Compila el firmware:
   ```sh
   make clean && make -j8 all
   ```

![Compilación del firmware](https://github.com/ccyl13/Proxmark3/blob/main/comando%20help.png?raw=true)

---

## 🔹 5. Flasheo del Proxmark3
1. Flashear el **Bootrom**:
   ```sh
   ./pm3-flash-bootrom
   ```

![Flasheo Bootrom](https://github.com/ccyl13/Proxmark3/blob/main/flasheo.png?raw=true)

2. **IMPORTANTE:** Después del primer flasheo, el número de puerto COM puede cambiar. Para comprobarlo, revisa el **Administrador de dispositivos** y localiza el nuevo puerto COM. Una vez identificado, flashea nuevamente el firmware con el nuevo COM asignado.

![Cambio de COM y reintento](https://github.com/ccyl13/Proxmark3/blob/main/cambia%20de%20com%20y%20se%20vuelve%20a%20flashear.png?raw=true)

3. Flashear el **Firmware completo**:
   ```sh
   ./pm3-flash-fullimage -p COM5
   ```
---

## 🔹 6. Uso del Cliente Proxmark3
1. Inicia el cliente Proxmark3:
   ```sh
   ./pm3
   ```

![Inicio del cliente Proxmark3](https://github.com/ccyl13/Proxmark3/blob/main/iniciamos%20el%20cliente.png?raw=true)

2. Para ver los comandos disponibles:
   ```sh
   help
   ```

![Lista de comandos](https://github.com/ccyl13/Proxmark3/blob/main/comando%20help.png?raw=true)

---

## 🔹 8. Ataques y Clonación de Tarjetas
📌 **Ejecutar ataque a una tarjeta Mifare 1K:**
```sh
hf mf autopwn
```

![Ataque hf mf autopwn](https://github.com/ccyl13/Proxmark3/blob/main/ataque.png?raw=true)

📌 **Resultados del ataque:**

![Ejecución de autopwn](https://github.com/ccyl13/Proxmark3/blob/main/ataque2.png?raw=true)

📌 **Clonación de tarjeta:**
```sh
hf mf cload -f <archivo-dump>
```
---

## 🔹 9. Conclusión

¡Ahora tienes tu **Proxmark3** configurado y listo para pruebas! 🎉

Para más información, revisa la documentación oficial:
- [Wiki de Proxmark3](https://github.com/RfidResearchGroup/proxmark3/wiki)
![CUID CARD](https://github.com/ccyl13/Proxmark3/blob/main/tarjeta%20CUID.jpeg?raw=true)
![RFID](https://github.com/ccyl13/Proxmark3/blob/main/RFID.jpeg?raw=true)

