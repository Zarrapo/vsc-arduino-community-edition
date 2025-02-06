# Extensión de Visual Studio Code para Arduino

> 💡Este documento contiene simplemente una traducción al español de la descripción del orginal en inglés.

[Repositorio en GitHub](https://github.com/vscode-arduino/vscode-arduino).  

**NOTA:** Esta es una bifurcación mantenida por la comunidad de la extensión de Arduino de Microsoft para VS Code.  

## **Introducción**  

¡Bienvenido a la extensión de Visual Studio Code para Arduino! Esta extensión facilita el desarrollo, la compilación y la carga de **sketches de Arduino** en VS Code, proporcionando un conjunto de funcionalidades avanzadas, tales como:  

✅ **IntelliSense** y resaltado de sintaxis para sketches de Arduino.  
✅ **Verificación y carga** de sketches dentro de VS Code.  
✅ **Gestor de placas y librerías** integrado.  
✅ **Lista de ejemplos** incorporada.  
✅ **Monitor serie** integrado.  
✅ **Snippets** para sketches.  
✅ **Estructura automática** de proyectos de Arduino.  
✅ **Integración con la paleta de comandos** (`F1`), permitiendo acceso rápido a funciones comunes como verificar y cargar sketches.  

---

## **Requisitos previos**  

Para usar esta extensión, se requiere **Arduino CLI** o el **Arduino IDE clásico**. Sin embargo, se recomienda utilizar la versión de **Arduino CLI incluida en la extensión**, ya que funciona automáticamente.  
📌 **Nota:** El soporte para el Arduino IDE clásico será eliminado en futuras versiones de la extensión.  

---

## **Configuración de Arduino CLI**  

Para utilizar la versión de **Arduino CLI integrada en la extensión**, asegúrate de que:  

1. La opción `arduino.useArduinoCli` esté configurada en `true`.  
2. Los valores `arduino.path` y `arduino.commandPath` estén vacíos o sin definir.  

Por defecto, `arduino.useArduinoCli` está en `false`, ya que la extensión aún mantiene soporte para el **Arduino IDE clásico**, pero se recomienda cambiarlo a `true`. La primera vez que se active la extensión, se solicitará la migración a **Arduino CLI**.  

Si prefieres utilizar una versión personalizada de **Arduino CLI**, puedes descargarla desde el repositorio oficial de Arduino. En ese caso, debes establecer `arduino.path` apuntando a la carpeta que contiene el ejecutable de Arduino CLI.  

---

## **Uso del Arduino IDE Clásico (No recomendado)**  

El uso del **Arduino IDE clásico** no es recomendable, y su soporte será eliminado en futuras versiones. Si aún deseas instalarlo, puedes hacerlo desde la página oficial de Arduino.  

📌 **Versiones compatibles:** Solo se admiten las versiones **1.6.x hasta 1.8.x**.  
🚫 **Versiones no soportadas:**  

- **Arduino IDE 2.x** no es compatible con esta extensión.  
- **La versión de la Microsoft Store no es compatible**, debido a su entorno de ejecución restringido (sandbox).  
- **Arduino IDE 1.8.7 tuvo fallos importantes**, solucionados en la versión **1.8.8 y posteriores**.  

---

## **Instalación de la extensión en VS Code**  

1. Abre **VS Code** y presiona `F1` o `Ctrl + Shift + P` (`Cmd + Shift + P` en Mac).  
2. Busca `Install Extension` e introduce:  

   ```cmd
   vscode-arduino-community
   ```

3. También puedes instalarla desde la **Microsoft Marketplace** buscando `Arduino`.  

---

## **Comandos disponibles en VS Code**  

La extensión proporciona varios comandos accesibles desde la **Paleta de Comandos** (`F1` o `Ctrl + Shift + P`):  

- **Arduino: Board Manager** → Gestiona paquetes de placas. Se pueden añadir placas de terceros configurando **Additional Board Manager URLs**.  
- **Arduino: Change Board Type** → Cambia la placa o plataforma utilizada.  
- **Arduino: Change Timestamp Format** → Cambia el formato de los registros en el **Monitor Serie**.  
- **Arduino: Close Serial Monitor** → Cierra el monitor serie y libera el puerto serie.  
- **Arduino: Examples** → Muestra la lista de ejemplos.  
- **Arduino: Initialize** → Configura un proyecto de Arduino en VS Code.  
- **Arduino: Library Manager** → Explora y gestiona librerías.  
- **Arduino: Open Serial Monitor** → Abre el **monitor serie** en la ventana integrada.  
- **Arduino: Select Serial Port** → Cambia el puerto serie actualmente en uso.  
- **Arduino: Upload** → Compila y sube el sketch a la placa.  
- **Arduino: CLI Upload** → Sube el código compilado sin recompilar (solo CLI).  
- **Arduino: Upload Using Programmer** → Sube el código utilizando un programador externo.  
- **Arduino: CLI Upload Using Programmer** → Sube el código precompilado con un programador externo (solo CLI).  
- **Arduino: Verify** → Compila el sketch sin subirlo a la placa.  
- **Arduino: Rebuild IntelliSense Configuration** → Fuerza la reconstrucción manual de la configuración de **IntelliSense** para corregir problemas de autocompletado.  

---

## **Atajos de teclado**  

- **Subir código:** `Alt + Cmd + U` (Mac) o `Alt + Ctrl + U` (Windows/Linux).  
- **Verificar código:** `Alt + Cmd + R` (Mac) o `Alt + Ctrl + R` (Windows/Linux).  
- **Reconstruir IntelliSense:** `Alt + Cmd + I` (Mac) o `Alt + Ctrl + I` (Windows/Linux).  

---

## **Opciones de configuración en VS Code**  

Se pueden configurar distintas opciones en `settings.json` dentro de VS Code:  

| Opción                        | Descripción |
|--------------------------------|-------------|
| `arduino.useArduinoCli`       | Define si se usa **Arduino CLI** (`true`) o el **Arduino IDE clásico** (`false`). Predeterminado: `false`. |
| `arduino.path`                | Ruta a la instalación de Arduino. Si se usa un IDE personalizado, se debe establecer aquí. |
| `arduino.commandPath`         | Ruta al ejecutable o script de Arduino. En Windows suele ser `arduino_debug.exe`. |
| `arduino.additionalUrls`      | URLs adicionales para el **gestor de placas**. |
| `arduino.logLevel`            | Nivel de salida de la CLI (`info` o `verbose`). Predeterminado: `info`. |
| `arduino.clearOutputOnBuild`  | Borra los registros antes de compilar o subir código. Predeterminado: `false`. |
| `arduino.enableUSBDetection`  | Activa la detección automática de USB. Predeterminado: `true`. |
| `arduino.disableTestingOpen`  | Desactiva el envío de mensajes de prueba al puerto serie. Predeterminado: `false`. |
| `arduino.analyzeOnOpen`       | Ejecuta el análisis automáticamente al abrir un proyecto. Predeterminado: `true`. |

---

## **Consideraciones finales**  

- Para asegurar la mejor compatibilidad, se recomienda **usar Arduino CLI en lugar del Arduino IDE clásico**.  
- **Arduino IDE 2.x no es compatible** con esta extensión, por lo que no se recomienda instalarlo si planeas trabajar con VS Code.  
- Si tienes problemas con **IntelliSense**, puedes reconstruir la configuración usando `Arduino: Rebuild IntelliSense Configuration`.  
- Puedes contribuir al desarrollo de la extensión a través del repositorio en GitHub.  

---

## **Licencia y código abierto**  

Esta extensión está licenciada bajo **MIT License** y es mantenida por la comunidad. Puedes encontrar más información en su [repositorio en GitHub](https://github.com/vscode-arduino/vscode-arduino).  

---
