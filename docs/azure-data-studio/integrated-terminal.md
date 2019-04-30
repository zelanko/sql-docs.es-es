---
title: Terminal integrado
titleSuffix: Azure Data Studio
description: Obtenga información sobre el terminal integrado en Azure Data Studio.
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 6677119a35d1d51ac8b6563d9bd9b9f32668c273
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63239383"
---
# <a name="integrated-terminal"></a>Terminal integrado

En [!INCLUDE[name-sos](../includes/name-sos-short.md)], puede abrir un terminal integrado, inicialmente desde la raíz del área de trabajo. Esto puede ser conveniente, ya que no tiene que cambiar windows o modificar el estado de un terminal existente para realizar una tarea de línea de comandos rápida.

Para abrir el terminal:

* Use la **Ctrl +'** método abreviado de teclado con el carácter de acento grave.
* Use la **vista** | **Terminal integrado** comando de menú.
* Desde el **paleta de comandos** (**Ctrl + Mayús + P**), use el **Terminal integrado: Alternar vista** comando.

![Terminal](media/integrated-terminal/terminal-screen.png)

> [!NOTE]
> Todavía puede abrir un shell externo con el Explorador de **abrir en símbolo** comando (**abrir en Terminal** en Mac o Linux) si prefiere trabajar fuera [!INCLUDE[name-sos](../includes/name-sos-short.md)].

## <a name="managing-multiple-terminals"></a>Administrar varios terminales

Puede crear varios terminales abierto a diferentes ubicaciones y navegar fácilmente entre ellos. Se pueden agregar instancias terminales pulsando el icono del signo más en la parte superior derecha de la **TERMINAL** panel o a desencadenar la **Ctrl + Mayús +'** comando. Esto crea otra entrada en la lista desplegable que se puede usar para cambiar entre ellas.

![Varios terminales](media/integrated-terminal/terminal-multiple-instances.png)

Pueden botón Quitar instancias terminales presionando la Papelera.

> [!TIP]
> Si usa varios terminales ampliamente, puede agregar enlaces de teclado para el `focusNext`, `focusPrevious` y `kill` comandos que se describen en la [sección de enlaces de teclado](#key-bindings) permitir la navegación entre ellas usando únicamente el teclado.

## <a name="configuration"></a>Configuración

El shell usa el valor predeterminado es `$SHELL` en Linux y macOS, PowerShell en Windows 10 y cmd.exe en versiones anteriores de Windows. Se pueden invalidar manualmente estableciendo `terminal.integrated.shell.*` en [configuración](settings.md). Se pueden pasar argumentos al shell de terminal en Linux y macOS usando el `terminal.integrated.shellArgs.*` configuración.

### <a name="windows"></a>Windows

Configurar correctamente el shell de Windows es una cuestión de localizar el archivo ejecutable correcto y actualizar la configuración. A continuación se muestran una lista de los archivos ejecutables de shell comunes y sus ubicaciones predeterminadas:

```json
// 64-bit cmd if available, otherwise 32-bit
"terminal.integrated.shell.windows": "C:\\Windows\\sysnative\\cmd.exe"
// 64-bit PowerShell if available, otherwise 32-bit
"terminal.integrated.shell.windows": "C:\\Windows\\sysnative\\WindowsPowerShell\\v1.0\\powershell.exe"
// Git Bash
"terminal.integrated.shell.windows": "C:\\Program Files\\Git\\bin\\bash.exe"
// Bash on Ubuntu (on Windows)
"terminal.integrated.shell.windows": "C:\\Windows\\sysnative\\bash.exe"
```

> [!NOTE]
> Para su uso como un terminal integrado, el ejecutable de shell debe ser una aplicación de consola para que `stdin/stdout/stderr` se pueden redirigir.

> [!TIP]
> Se está ejecutando el shell de terminal integrado con los permisos de [!INCLUDE[name-sos](../includes/name-sos-short.md)]. Si necesita ejecutar un comando de shell con privilegios elevados (Administrador) o permisos diferentes, puede usar las utilidades de la plataforma, como `runas.exe` dentro de una ventana de terminal.

### <a name="shell-arguments"></a>Argumentos de shell

Puede pasar argumentos al shell cuando se inicia.

Por ejemplo, para habilitar la ejecución de bash como un shell de inicio de sesión (que se ejecuta `.bash_profile`), pasar la `-l` argumento (con comillas dobles):

```json
// Linux
"terminal.integrated.shellArgs.linux": ["-l"]
```

## <a name="terminal-display-settings"></a>Configuración de pantalla de Terminal

Puede personalizar la fuente de terminal integrado y el alto de línea con la siguiente configuración:

* `terminal.integrated.fontFamily`
* `terminal.integrated.fontSize`
* `terminal.integrated.lineHeight`

## <a id="key-bindings"></a>Enlaces de teclado de Terminal

El **vista: Alternar Terminal integrado** comando está enlazado a **Ctrl +'** alternar rápidamente el panel de terminal integrado dentro y fuera de la vista.

A continuación se muestran los métodos abreviados de teclado para desplazarse rápidamente dentro el terminal integrado:

Key|Comando
---|---
**CTRL +'**| Mostrar el terminal integrado
**CTRL + MAYÚS +'**| Crear nueva terminal
**Ctrl+flecha arriba**|Desplácese hacia arriba
**Ctrl+flecha abajo**|Desplácese hacia abajo
**Ctrl+PageUp**|Desplazar página hacia arriba
**Ctrl+PageDown**|Desplazar página hacia abajo
**CTRL + Inicio**|Desplácese hasta la parte superior
**CTRL + fin**|Desplácese hacia abajo
**CTRL + K**|Desactive el terminal

Otros comandos de terminal están disponibles y se pueden enlazar a los métodos abreviados de teclado preferido.

Estas sobrecargas son:

* `workbench.action.terminal.focus`: Centrar el terminal. Esto es similar a alternar pero centra el terminal en lugar de ocultarlo, si está visible.
* `workbench.action.terminal.focusNext`: Se centra en la siguiente instancia de terminal.
* `workbench.action.terminal.focusPrevious`: Se centra en la instancia anterior de terminal.
* `workbench.action.terminal.kill`: Quite la instancia actual de terminal.
* `workbench.action.terminal.runSelectedText`: Ejecute el texto seleccionado en la instancia de terminal.
* `workbench.action.terminal.runActiveFile`: Ejecute el archivo activo en la instancia de terminal.

### <a name="run-selected-text"></a>Ejecutar texto seleccionado

Para usar el `runSelectedText` de comandos, seleccione el texto en un editor y ejecute el comando **Terminal: Ejecutar texto seleccionado en el Terminal Active** a través de la **paleta de comandos** (**Ctrl + Mayús + P**). El terminal intenta ejecutar el texto seleccionado:

![Ejecutar texto seleccionado](media/integrated-terminal/terminal_run_selected.png)

Si no hay texto seleccionado en el editor activo, se ejecuta la línea donde se encuentra el cursor en el terminal.

### <a name="copy--paste"></a>Copiar y pegar

Los enlaces de teclado para copiar y pegar siguen los estándares de la plataforma:

* Linux: **CTRL + MAYÚS + C** y **Ctrl + Mayús + V**
* Mac: **Cmd + C** y **Cmd + V**
* Windows: **CTRL + C** y **Ctrl + V**

### <a name="find"></a>Buscar

El Terminal integrado ofrece la funcionalidad de búsqueda básica que se puede desencadenar con **CTRL+f**.

Si desea que **CTRL+f** para ir al shell en lugar de iniciar el widget de búsqueda en Linux y Windows, deberá quitar el enlace de teclado de este modo:

```js
{ "key": "ctrl+f", "command": "-workbench.action.terminal.focusFindWidget",
                      "when": "terminalFocus" },
```

### <a name="rename-terminal-sessions"></a>Cambiar el nombre de sesiones de terminal Server

Sesiones de Terminal integradas ahora se pueden cambiar mediante la **Terminal: Cambiar el nombre de** (`workbench.action.terminal.rename`) comando. El nuevo nombre se muestra en la lista desplegable de selección terminal.

### <a name="forcing-key-bindings-to-pass-through-the-terminal"></a>Forzar los enlaces de teclado para pasar a través del terminal

Mientras el foco está en el terminal integrado, muchos de los enlaces de teclado no funcionarán porque se pasan a las pulsaciones de teclas y se consume el terminal propio. El `terminal.integrated.commandsToSkipShell` opción puede usarse para solucionar este problema. Contiene una matriz de nombres de comando cuyos enlaces claves omitir el procesamiento, el shell y en su lugar se procesó el [!INCLUDE[name-sos](../includes/name-sos-short.md)] sistema de enlace de clave. De forma predeterminada, esto incluye todos los enlaces de teclado de terminales además un Seleccione algunas frecuente los enlaces de teclado.

