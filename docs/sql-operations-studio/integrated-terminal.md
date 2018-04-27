---
title: Terminal integrada en las operaciones de SQL Studio (versión preliminar) | Documentos de Microsoft
description: Obtenga información sobre el terminal integrado en las operaciones de SQL Studio (versión preliminar).
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: article
author: yualan
ms.author: alayu
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 61d74e7d8818391ca01c45ad8f9a7b2897751712
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="integrated-terminal"></a>Terminal integrado

En [!INCLUDE[name-sos](../includes/name-sos-short.md)], puede abrir un terminal integrado, inicialmente a partir de la raíz del área de trabajo. Esto puede ser cómodo, ya que no tiene que cambiar las ventanas o se altera el estado de un terminal existente para realizar una tarea de línea de comandos rápida.

Para abrir el terminal:

* Use la **Ctrl +'** método abreviado de teclado con el carácter de acento grave.
* Use la **vista** | **Terminal integrado** comando de menú.
* Desde el **comando paleta** (**Ctrl + Mayús + P**), use la **Terminal integrado de vista: alternar** comando.

![Terminal](media/integrated-terminal/terminal-screen.png)

> [!NOTE]
> Todavía puede abrir un shell externo con el Explorador de **abrir en el símbolo del sistema** comando (**abrir en Terminal** en Mac o Linux) si prefiere trabajar fuera [!INCLUDE[name-sos](../includes/name-sos-short.md)].

## <a name="managing-multiple-terminals"></a>Administrar varios terminales

Puede crear varios terminales abierto a diferentes ubicaciones y navegar fácilmente entre ellos. Se pueden agregar instancias de Terminal cuando se alcanza el icono del signo más en la parte superior derecha de la **TERMINAL** panel o por desencadena la **Ctrl + Mayús +'** comando. Esto crea otra entrada en la lista desplegable que puede utilizarse para cambiar entre ellos.

![Varios terminales](media/integrated-terminal/terminal-multiple-instances.png)

Pueden botón Quitar instancias terminal presionando la Papelera.

> [!TIP]
> Si usa varios terminales ampliamente, puede agregar enlaces de teclado para la `focusNext`, `focusPrevious` y `kill` comandos que se describen en la [sección de enlaces de clave](#key-bindings) para permitir la navegación entre ellos utilizando únicamente el teclado.

## <a name="configuration"></a>Configuración

El shell usa el valor predeterminado es `$SHELL` en Linux y macOS, PowerShell en Windows 10 y cmd.exe en versiones anteriores de Windows. Éstos pueden invalidar manualmente estableciendo `terminal.integrated.shell.*` en [configuración](settings.md). Argumentos se pueden pasar al shell de terminal en Linux y macOS utilizando el `terminal.integrated.shellArgs.*` configuración.

### <a name="windows"></a>Windows

Configurar correctamente el shell de Windows consiste en buscar el archivo ejecutable correcto y actualizar la configuración. A continuación se muestran una lista de los archivos ejecutables de shell comunes y sus ubicaciones predeterminadas:

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
> Para poder usarse como un terminal integrado, el ejecutable de shell debe ser una aplicación de consola para que `stdin/stdout/stderr` se pueden redirigir.

> [!TIP]
> El shell integrado de terminal se ejecuta con los permisos de [!INCLUDE[name-sos](../includes/name-sos-short.md)]. Si tiene que ejecutar un comando de shell con permisos diferentes o con permisos elevados (Administrador), puede usar las utilidades de plataforma como `runas.exe` dentro de un terminal.

### <a name="shell-arguments"></a>Argumentos de shell

Puede pasar argumentos al shell cuando se inicia.

Por ejemplo, para habilitar la ejecución intensiva de errores como un shell de inicio de sesión (que se ejecuta `.bash_profile`), pase el `-l` argumento (con comillas dobles):

```json
// Linux
"terminal.integrated.shellArgs.linux": ["-l"]
```

## <a name="terminal-display-settings"></a>Configuración de pantalla de Terminal

Puede personalizar la fuente de terminal integrado y el alto de línea con la configuración siguiente:

* `terminal.integrated.fontFamily`
* `terminal.integrated.fontSize`
* `terminal.integrated.lineHeight`

## <a id="key-bindings"></a>Enlaces de teclado de Terminal

El **vista: alternar integrado Terminal** comando está enlazado a **Ctrl +'** para cambiar rápidamente el panel integrado terminal u ocultar.

A continuación se muestran los métodos abreviados de teclado para desplazarse rápidamente dentro de la terminal integrada:

Key|Comando
---|---
**CTRL +'**|Mostrar terminal integrado
**CTRL + MAYÚS +'**|Crear nueva terminal
**Ctrl+flecha arriba**|Desplazarse hacia arriba
**Ctrl+flecha abajo**|Desplácese hacia abajo
**CTRL + RE PÁG**|Desplazamiento Re Pág
**CTRL + AV PÁG**|Página de desplazamiento hacia abajo
**CTRL + Inicio**|Desplácese hasta la parte superior
**CTRL + fin**|Desplácese hasta la parte inferior
**CTRL + K**|Desactive el terminal

Otros comandos terminal están disponibles y se pueden enlazar a los métodos abreviados de teclado preferido.

Estas sobrecargas son:

* `workbench.action.terminal.focus`: Se centran el terminal. Esto es similar a alternar pero centra el terminal en lugar de ocultar, si está visible.
* `workbench.action.terminal.focusNext`: Se centra en la siguiente instancia de terminal.
* `workbench.action.terminal.focusPrevious`: Se centra en la instancia anterior de terminal.
* `workbench.action.terminal.kill`: Quita la instancia actual de terminal.
* `workbench.action.terminal.runSelectedText`: Ejecutar el texto seleccionado en la instancia de terminal.
* `workbench.action.terminal.runActiveFile`: Ejecute el archivo activo en la instancia del terminal.

### <a name="run-selected-text"></a>Ejecutar texto seleccionado

Para usar el `runSelectedText` de comandos, seleccionar texto en un editor y ejecute el comando **Terminal: ejecutar texto seleccionado en Terminal Active** a través de la **comando paleta** (**Ctrl + Mayús + P**). El terminal intenta ejecutar el texto seleccionado:

![Ejecutar texto seleccionado](media/integrated-terminal/terminal_run_selected.png)

Si no hay texto seleccionado en el editor activo, la línea que el cursor está en se ejecuta en el terminal.

### <a name="copy--paste"></a>Copiar y pegar

Los enlaces de teclado para copiar y pegar, siga los estándares de plataforma:

* Linux: **Ctrl + Mayús + C** y **Ctrl + Mayús + V**
* Mac: **Cmd + C** y **Cmd + v.**
* Windows: **Ctrl + C** y **Ctrl + v.**

### <a name="find"></a>Buscar

El Terminal integrado dispone de funcionalidad de búsqueda básica que se puede activar con **CTRL+f**.

Si desea que **CTRL+f** para ir al shell en lugar de iniciar el widget de búsqueda en Linux y Windows, es necesario quitar el keybinding así:

```js
{ "key": "ctrl+f", "command": "-workbench.action.terminal.focusFindWidget",
                      "when": "terminalFocus" },
```

### <a name="rename-terminal-sessions"></a>Cambiar el nombre de sesiones de terminal Server

Sesiones de Terminal Server integradas ahora se pueden cambiar mediante la **Terminal: cambiar el nombre de** (`workbench.action.terminal.rename`) comando. El nuevo nombre se muestra en la lista desplegable de selección de terminal.

### <a name="forcing-key-bindings-to-pass-through-the-terminal"></a>Forzar los enlaces de teclado para pasar a través del terminal

Mientras el foco está en el terminal integrado, muchos enlaces de teclado no funcionarán porque se pasan a las pulsaciones de tecla y se consume el terminal propio. El `terminal.integrated.commandsToSkipShell` opción puede usarse para evitar esto. Contiene una matriz de nombres de comando cuyos enlaces claves omitir procesamiento el shell y en su lugar ser procesados por el [!INCLUDE[name-sos](../includes/name-sos-short.md)] sistema de enlace de clave. De forma predeterminada, esto incluye todos los enlaces de teclado de terminal además un seleccione enlaces de clave utilizadas algunos.

