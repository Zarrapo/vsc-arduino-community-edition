# Configuración Visual Studio Code con la Extesión para Arduino

## Introducción

Este documento proporciona una guía detallada para configurar y utilizar Visual Studio Code (VS Code) en Windows con la extensión Arduino para desarrollar y programar placas Arduino en sistemas Windows. Se centra en la solución de problemas comunes y proporciona los comandos necesarios para listar placas y encontrar el puerto COM utilizado.

## 1. Requisitos previos

- **Windows 10/11**
- **Visual Studio Code** instalado
- **Arduino CLI** instalado
- **Extensión de Arduino para VS Code** instalada
- Placa Arduino: **Arduino Uno**

> 💡 Se recomienda usar una placa original durante la primera configuración para evitar problemas de drivers, en su defecto asegúrate de tener instalados adecuadamente los drivers de tu placa. Aunque el "Arduino IDE" reconozca una placa no garantiza que la extensión también la reconozca.

## 2. Instalación de Arduino CLI

### 2.1 Descargar e instalar Arduino CLI

1. Descarga Arduino CLI desde la página oficial:
   - [https://github.com/arduino/arduino-cli/releases/tag/v1.1.1](https://github.com/arduino/arduino-cli/releases/tag/v1.1.1)
2. Selecciona la versión adecuada:
   - **`arduino-cli_1.1.1_Windows_64bit.msi`** → Instalador automático que configura el Path automáticamente.
   - **`arduino-cli_1.1.1_Windows_64bit.zip`** → Requiere configuración manual del Path.
3. Si descargas la versión `.zip`, extrae el archivo en una ubicación accesible, por ejemplo:

   ```cmd
   C:\arduino-cli
   ```

4. Si usaste la versión `.zip`, agrega manualmente la ruta al **Path** del sistema:
   - Abre **Ejecutar** (`Win + R`), escribe `sysdm.cpl` y presiona `Enter`.
   - Ve a **Opciones avanzadas > Variables de entorno**.
   - En "Variables del sistema", busca `Path` y haz clic en **Editar**.
   - Agrega `C:\arduino-cli`.

### 2.2 Verificar la instalación

Abre una **terminal** y ejecuta:

```cmd
arduino-cli version
```

Debería mostrar algo similar a:

```cmd
arduino-cli  Version: 1.1.1 Commit: fa6eafcb Date: 2024-11-22T09:31:38Z
```

## 3. Configuración en VS Code

### 3.1 Instalar la extensión de Arduino

![Arduino Community Edition](https://raw.githubusercontent.com/Zarrapo/vsc-arduino-community-edition/refs/heads/main/images/Extension.png)

1. Abre **Visual Studio Code**.
2. Ve a **Extensiones** (`Ctrl+Shift+X`).
3. Busca `Arduino` e instala **Arduino Community Edition**.

### 3.2 Configurar Arduino CLI en VS Code

1. Abre la configuración (`Ctrl+,`).
2. Si deseas usar la versión integrada de Arduino CLI, **deja vacío** `Arduino: Path` y `Arduino: Command Path`.
3. Si prefieres usar una versión instalada manualmente, configura `Arduino: Path` con la ruta correspondiente, por ejemplo:

   ```cmd
   C:\arduino-cli
   ```

4. Asegúrate de que `Arduino: Use Arduino CLI` esté activado.
5. Guarda y reinicia VS Code.

## 4. Identificar la placa y el puerto COM

### 4.1 Listar las placas conectadas

Ejecuta desde el terminal:

```sh
arduino-cli board list
```

Salida esperada:

```cmd
Puerto  Protocolo  Tipo              Nombre de la placa  FQBN            Núcleo
COM5    serial     Serial Port (USB) Arduino Uno        arduino:avr:uno arduino:avr
```

### 4.2 Seleccionar la placa en VS Code

1. Abre la **paleta de comandos** (`Ctrl+Shift+P`).
2. Escribe `Arduino: Select Board` y elige tu placa.

### 4.3 Seleccionar el puerto COM en VS Code

1. Abre la **paleta de comandos** (`Ctrl+Shift+P`).
2. Escribe `Arduino: Select Serial Port` y elige el puerto detectado (`COM5` en  nuestro caso).

## 5. Compilar y subir un sketch

### 5.1 Crear un archivo `.ino`

En VS Code, crea un archivo `C:\Blink\Blink.ino` con el siguiente código:

```cpp
void setup() {
  pinMode(LED_BUILTIN, OUTPUT);
}

void loop() {
  digitalWrite(LED_BUILTIN, HIGH);
  delay(1000);
  digitalWrite(LED_BUILTIN, LOW);
  delay(1000);
}
```

> El directorio padre de nuestro archivo de código `Blink.ino` se debe llamar igual `Blink`.

### 5.2 Compilar el sketch

Desde VS Code:

- Abre la **paleta de comandos** (`Ctrl+Shift+P`).
- Escribe `Arduino: Verify` (`Ctrl+Alt+R`).

> También podemos utilizar los botones de la interfaz de VSC.

### 5.3 Subir el sketch

- Abre la **paleta de comandos** (`Ctrl+Shift+P`).
- Escribe `Arduino: Upload` (`Ctrl+Alt+U`).
- Verifica que la salida indique que el código se subió correctamente.

## 6. Solución de problemas

### 6.1 `arduino-cli` no es reconocido

Si en el terminal vemos:

```terminal
arduino-cli: The term 'arduino-cli' is not recognized as a name...
```

Prueba:

```sh
where arduino-cli
```

Si no aparece la ruta correcta, verifica que **`arduino-cli.exe` esté en el Path**.

### 6.2 No se detecta la placa Arduino

1. Verifica la conexión USB.
2. Usa `arduino-cli board list` para confirmar el puerto.
3. Si es un clon de Arduino, instala los drivers **CH340**.

### 6.3 No se puede seleccionar la placa en VS Code

- Abre `arduino.json` en VS Code (`Arduino: Board Configuration`) y configúralo manualmente:

  ```json
  {
    "arduino.fqbn": "arduino:avr:uno",
    "arduino.port": "COM5"
  }
  ```

- Guarda y reinicia VS Code.  
  