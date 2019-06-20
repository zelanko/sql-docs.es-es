---
title: 'Tutorial: Creación de una extensión'
titleSuffix: Azure Data Studio
description: Este tutorial muestra cómo crear una extensión para agregar funcionalidad personalizada a Azure Data Studio.
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: tutorial
author: kevcunnane
ms.author: kcunnane
manager: jroth
ms.openlocfilehash: 2f031ec68cc6ae342b8bac51c450ee40a9df0555
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66797959"
---
# <a name="tutorial-create-an-azure-data-studio-extension"></a>Tutorial: Crear una extensión de Azure Data Studio

Este tutorial muestra cómo crear una nueva extensión de Azure Data Studio. La extensión crea los enlaces de teclado de SSMS conocidos en Azure Data Studio.

Durante este tutorial obtendrá información sobre cómo:
> [!div class="checklist"]
> * Crear un proyecto de extensión
> * Instalar el generador de extensión
> * Crear su extensión
> * Probar la extensión
> * Empaquetar la extensión
> * Publicar la extensión en marketplace

## <a name="prerequisites"></a>Requisitos previos

Azure Data Studio se basa en el mismo marco de trabajo como código de Visual Studio, por lo que se crean las extensiones de Azure Data Studio con Visual Studio Code. Para empezar, necesita los siguientes componentes:

- [Node.js](https://nodejs.org) instalados y disponibles en su `$PATH`. Node.js incluye [npm](https://www.npmjs.com/), el Administrador de paquetes de Node.js que se usa para instalar el generador de extensión.
- [Código de Visual Studio](https://code.visualstudio.com) para depurar la extensión.
- Los datos de Azure Studio [depurar extensión](https://marketplace.visualstudio.com/items?itemName=ms-mssql.sqlops-debug) (opcional). Esto le permite probar la extensión sin necesidad de paquete e instalarlo en Azure Data Studio.
- Asegúrese de `azuredatastudio` en su ruta. Para Windows, asegúrese de elegir el `Add to Path` opción en setup.exe. Para Mac o Linux, ejecute el *instalar el comando 'azuredatastudio' en la ruta de acceso* opción.


## <a name="install-the-extension-generator"></a>Instalar el generador de extensión

Para simplificar el proceso de creación de extensiones, hemos creado un [generador extensión](https://code.visualstudio.com/docs/extensions/yocode) mediante Yeoman. Para instalarlo, ejecute lo siguiente desde el símbolo del sistema:

`npm install -g yo generator-azuredatastudio`

## <a name="create-your-extension"></a>Crear su extensión

Para crear una extensión:

1. Inicie el generador de extensión con el siguiente comando:

   `yo azuredatastudio`

2. Elija **nuevo mapa de teclas** en la lista de tipos de extensión:

   ![Generador de extensión](./media/tutorial-create-extension/extension-generator.png)

3. Siga los pasos necesarios para que rellene el nombre de extensión (para este tutorial, use **ssmskeymap2**) y agregar una descripción.

Completar los pasos anteriores, crea una nueva carpeta. Abra la carpeta de código de Visual Studio y está listo para crear su propia extensión de enlace de teclado.


### <a name="add-a-keyboard-shortcut"></a>Agregar un método abreviado de teclado

**Paso 1: Buscar los métodos abreviados para reemplazar**

Ahora que tenemos nuestra extensión preparado para comenzar, agregue algunos métodos abreviados de teclado SSMS (o enlaces de teclado) en Azure Data Studio. He usado [hoja de referencia de Andy Mallon](https://am2.co/2018/02/updated-cheat-sheet/) y lista de métodos abreviados de teclado de RedGate para inspirarse.

Eran las cosas principales que VI que faltan:

- Ejecutar una consulta con el plan de ejecución real habilitado. Se trata de **Ctrl + M** en SSMS y no tiene un enlace en Azure Data Studio.
- Tener **CTRL + MAYÚS + E** como una segunda forma de ejecutar una consulta. Comentarios de los usuarios indican que esto era que faltan.
- Tener **ALT + F1** ejecutar `sp_help`. Agregamos esto en Azure Data Studio, pero dado que ese enlace ya estaba en uso, asignamos a **ALT + F2** en su lugar.
- Alternar pantalla completa (**MAYÚS + ALT + INTRO**).
- **F8** mostrar **Explorador de objetos** / **vista servidores**.

Es fácil buscar y reemplazar estos enlaces de teclado. Ejecute *abierto de métodos abreviados de teclado* para mostrar el **métodos abreviados de teclado** pestaña en Azure Data Studio, busque *consulta* y, a continuación, elija **enlacedecambiarlaclave**. Cuando haya terminado cambiar el enlace de teclado, puede ver la asignación actualizada en el archivo keybindings.json (ejecutar *abierto de métodos abreviados de teclado* para verlo).

![métodos abreviados de teclado](./media/tutorial-create-extension/keyboard-shortcuts.png)

![extensión KeyBindings.JSON](./media/tutorial-create-extension/keybindings-json.png)


**Paso 2: Agregar accesos directos a la extensión**

Para agregar accesos directos a la extensión, abra el *package.json* archivo (en la extensión) y reemplace el `contributes` sección con lo siguiente:

```json
"contributes": {
  "keybindings": [
    {
      "key": "shift+cmd+e",
      "command": "runQueryKeyboardAction"
    },
    {
      "key": "ctrl+cmd+e",
      "command": "workbench.view.explorer"
    },
    {
      "key": "alt+f1",
      "command": "workbench.action.query.shortcut1"
    },
    {
      "key": "shift+alt+enter",
      "command": "workbench.action.toggleFullScreen"
    },
    {
      "key": "f8",
      "command": "workbench.view.connections"
    },
    {
      "key": "ctrl+m",
      "command": "runCurrentQueryWithActualPlanKeyboardAction"
    }
  ]
}
```

## <a name="test-your-extension"></a>Probar la extensión

Asegúrese de `azuredatastudio` está en la ruta de acceso ejecutando el comando de instalación azuredatastudio en ruta de acceso en Azure Data Studio.

Asegúrese de que está instalada la extensión de Azure Data Studio depurar en Visual Studio Code.

Seleccione **F5** para iniciar Azure Data Studio en modo de depuración con la extensión que se ejecuta:

![Instalar extensión](./media/tutorial-create-extension/install-extension.png)

![extensión de prueba](./media/tutorial-create-extension/test-extension.png)

Mapas de claves son una de las extensiones más rápidas para crear, por lo que la nueva extensión debe ser ahora preparado para compartir y funcionan correctamente.

## <a name="package-your-extension"></a>Empaquetar la extensión

Para compartir con otros usuarios debe empaquetar la extensión en un único archivo. Esto puede ser publicado en el marketplace de extensiones de Azure Data Studio, o compartida entre su equipo o la Comunidad. Para ello, deberá instalar otro paquete de npm desde la línea de comandos:

`npm install -g vsce`

Navegue hasta el directorio base de la extensión y ejecute `vsce package`. Tuve que agregar un par de líneas adicionales para detener el *vsce* herramienta desde quejan:

```json
"repository": {
    "type": "git",
    "url": "https://github.com/kevcunnane/ssmskeymap.git"
},
"bugs": {
    "url": "https://github.com/kevcunnane/ssmskeymap/issues"
},
```

Una vez que esto se ha hecho, mi archivo ssmskeymap 0.1.0.vsix se ha creado y listo para instalar y compartir con todo el mundo!

![Instalar extensión](./media/tutorial-create-extension/extensions.png)


## <a name="publish-your-extension-to-the-marketplace"></a>Publicar la extensión en marketplace

El marketplace de extensiones de Azure Data Studio todavía no está totalmente implementado, pero el proceso actual es para hospedar la extensión de VSIX en algún lugar (por ejemplo, una página de la versión de GitHub), a continuación, envíe un PR actualizando [este archivo JSON](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json) con su información de la extensión.


## <a name="next-steps"></a>Pasos siguientes

En este tutorial ha aprendido a:
> [!div class="checklist"]
> * Crear un proyecto de extensión
> * Instalar el generador de extensión
> * Crear su extensión
> * Probar la extensión
> * Empaquetar la extensión
> * Publicar la extensión en marketplace


Esperamos que después de leerlo que estará lleno de inspiración para crear su propia extensión para Azure Data Studio. Contamos con compatibilidad con información de los paneles (gráficos más bonito del mundo que se ejecutan en el servidor SQL Server), un número de las API específicas de SQL y un enorme conjunto existente de puntos de extensión que se hereda de Visual Studio Code.

Si tiene una idea, pero no está seguro de cómo empezar, abra un problema o un tweet en el equipo: [azuredatastudio](https://twitter.com/azuredatastudio).

Siempre puede hacer referencia a la [Guía de la extensión de Visual Studio Code](https://code.visualstudio.com/docs/extensions/overview) porque abarca todas las API existentes y patrones.


Para obtener información sobre cómo trabajar con T-SQL en Azure Data Studio, complete el tutorial de T-SQL, Editor:

> [!div class="nextstepaction"]
> [Usar el editor de Transact-SQL para crear objetos de base de datos](tutorial-sql-editor.md).
