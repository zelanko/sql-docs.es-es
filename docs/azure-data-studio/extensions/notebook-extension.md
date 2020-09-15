---
title: Creación de una extensión de cuaderno de Jupyter Notebook
description: Obtenga información sobre cómo empaquetar cuadernos en una extensión mediante el generador de extensiones.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: how-to
author: yualan
ms.author: alayu
ms.reviewer: alayu, maghan
ms.custom: ''
ms.date: 08/28/2020
ms.openlocfilehash: 52a38a8074814737a30cb2f31d22da922eb76901
ms.sourcegitcommit: b6ee0d434b3e42384b5d94f1585731fd7d0eff6f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/02/2020
ms.locfileid: "89288157"
---
# <a name="create-a-jupyter-notebook-extension"></a>Creación de una extensión de cuaderno de Jupyter Notebook

En este tutorial se muestra cómo crear una extensión de Notebook de Azure Data Studio. La extensión envía un cuaderno de Jupyter Notebook de ejemplo que se puede abrir y ejecutar en Azure Data Studio.

Durante este tutorial aprenderá a realizar lo siguiente:
> [!div class="checklist"]
> - Creación de un proyecto de extensión
> - Instalación del generador de extensiones
> - Crear la extensión de cuaderno
> - Ejecutar la extensión
> - Empaquetado de la extensión
> - Publicación de la extensión en Marketplace

## <a name="apis-used"></a>API utilizadas

- `azdata.nb.showNotebookDocument`

### <a name="extension-use-cases"></a>Casos de uso de la extensión

Hay varias razones para crear una extensión de cuaderno: 
- Compartir documentación interactiva 
- Guardar y tener acceso constante a ese cuaderno
- Proporcionar problemas de codificación para que los usuarios los sigan
- Crear versiones y realizar el seguimiento de las actualizaciones del cuaderno

## <a name="prerequisites"></a>Prerrequisitos

Azure Data Studio se basa en el mismo marco que Visual Studio Code, por lo que las extensiones para Azure Data Studio se crean con Visual Studio Code. Para comenzar, necesitará los siguientes componentes:

- [Node.js](https://nodejs.org) instalado y disponible en su `$PATH`. Node.js incluye [npm](https://www.npmjs.com/), el administrador de paquetes de Node.js, que se usa para instalar el generador de extensiones.
- [Visual Studio Code](https://code.visualstudio.com) para depurar la extensión.
- Asegúrese de que `azuredatastudio` está en su ruta de acceso. En el caso de Windows, asegúrese de elegir la opción `Add to Path` de setup.exe. En Mac o Linux, ejecute la opción de *instalación del comando "azuredatastudio" de PATH*.

## <a name="install-the-extension-generator"></a>Instalación del generador de extensiones

Para simplificar el proceso de creación de extensiones, hemos compilado [un generador de extensiones](https://www.npmjs.com/package/generator-azuredatastudio) con Yeoman. Para instalarlo, ejecute lo siguiente desde el símbolo del sistema:

```console
`npm install -g yo generator-azuredatastudio`
```

## <a name="create-your-extension"></a>Creación de la extensión

Para crear una extensión:

1. Inicie el generador de extensiones con el siguiente comando:

   `yo azuredatastudio`

2. Elija **Nuevo cuaderno (individual)** en la lista de tipos de extensiones:

   :::image type="content" source="media/notebook-extension/notebook-extension-generator.png" alt-text="Generador de extensiones de cuaderno":::

3. Siga los pasos para rellenar el nombre de la extensión (para este tutorial, use **Cuaderno de prueba**), un nombre de publicador (para este tutorial, use **Microsoft**) y agregue una descripción.

Ahora, aquí es donde existen varias alternativas: puede agregar cuadernos de Jupyter Notebook que ya ha creado, o bien puede usar cuadernos de ejemplo que le haya proporcionado el generador.

En este tutorial, se usará un cuaderno de Python de ejemplo:

   :::image type="content" source="media/notebook-extension/notebook-sample-generator.png" alt-text="Selección del ejemplo de Python":::

Si tiene cuadernos que le interesa enviar, responda que tiene cuadernos que le gustaría enviar y proporcione la ruta de acceso absoluta a la ubicación de todos los cuadernos o archivos Markdown.

Al completar los pasos anteriores, se crea una carpeta con el cuaderno de ejemplo. Abra la carpeta en Visual Studio Code y estará listo para enviar la nueva extensión de cuaderno.

## <a name="understanding-your-extension"></a>Descripción de la extensión

Este es el aspecto que debe tener el proyecto:

   :::image type="content" source="media/notebook-extension/notebook-file-structure-generator.png" alt-text="Estructura de los archivos de la extensión":::

`vsc-extension-quickstart.md` proporciona una referencia de los archivos importantes. En `README.md` puede proporcionar documentación para la nueva extensión. Observe los archivos `package.json`, `notebook.ts` y `pySample.ipynb`.

Si hay archivos o carpetas que no quiere publicar, puede incluir sus nombres en el archivo `.vscodeignore`.

Ahora se examinará `notebook.ts` para comprender lo que hace la extensión recién creada.

```javascript
// This function is called when you run the command `Launch Notebooks: Test Notebook` from
// command palette in Azure Data Studio. If you would like any additional functionality
// to occur when you launch the book, add to the activate function.
export function activate(context: vscode.ExtensionContext) {
    context.subscriptions.push(vscode.commands.registerCommand('launchNotebooks.test-notebook', () => {
        let notebooksToDisplay: Array<string> = processNotebooks();
        notebooksToDisplay.forEach(name => {
            azdata.nb.showNotebookDocument(vscode.Uri.file(name));
        });
    }));

    // Add other code here if you want to register another command
}
```

Esta es la función principal de `notebook.ts` a la que se llama cada vez que se ejecuta la extensión mediante el comando, **Iniciar cuadernos: cuaderno de prueba**. El comando se crea mediante la API `vscode.commands.registerCommand` y la siguiente definición dentro de las llaves es el código que se ejecuta cada vez que se llama al comando. Cada cuaderno que se encuentre en la función `processNotebooks` se abre en Azure Data Studio mediante `azdata.nb.showNotebookDocument`. 

El archivo `package.json` también desempeña un papel importante en el registro del comando, **Iniciar cuadernos: cuaderno de prueba**.

```json
"activationEvents": [
        "onCommand:launchNotebooks.test-notebook"
    ],
    "main": "./out/notebook.js",
    "contributes": {
        "commands": [
            {
                "command": "launchNotebooks.test-notebook",
                "title": "Launch Notebooks: Test Notebook"
            }
        ]
    }
```

Hay un evento de activación para el comando y también se han agregado puntos de contribución específicos. Estos se muestran en el marketplace de extensiones, donde se publican las extensiones, cuando los usuarios consultan la extensión. Si quiere agregar comandos adicionales, asegúrese de hacerlo en el campo `activationEvents`. Para obtener más opciones, vea [Eventos de activación](https://code.visualstudio.com/api/references/activation-events).

## <a name="package-your-extension"></a>Empaquetado de la extensión

Para compartirla con otros usuarios, ha de empaquetar la extensión en un solo archivo. Este se puede publicar en el Marketplace de extensiones de Azure Data Studio o compartir entre su equipo o comunidad. Para ello, debe instalar otro paquete npm desde la línea de comandos:

```console
`npm install -g vsce`
```

Edite `README.md` como prefiera, vaya hasta el directorio base de la extensión y ejecute `vsce package`. Opcionalmente, puede vincular un repositorio con la extensión o continuar sin ninguno. Para agregar uno, agregue una línea similar al archivo `package.json`.

```json
"repository": {
    "type": "git",
    "url": "https://github.com/laurajjiang/testnotebook.git"
}
```

Después de hacer esto, se crea el archivo test-notebook-0.0.1.vsix y está listo para instalarlo y compartirlo con el mundo.

## <a name="run-your-extension"></a>Ejecución de la extensión

Para ejecutar y probar la extensión, abra Azure Data Studio y abra la paleta de comandos (`Ctrl + Shift + P`). Busque el comando **Extensiones: Instalar desde VSIX** y navegue hasta la carpeta que contiene la nueva extensión.

   :::image type="content" source="media/notebook-extension/install-vsix.png" alt-text="Instalación de VSIX":::

Ahora debería aparecer en el panel de extensiones de Azure Data Studio. Vuelva a abrir la paleta de comandos y encontrará el nuevo comando que se ha creado con la extensión, **Iniciar libro: libro de prueba**. Al ejecutarlo, debe abrir el libro de Jupyter que ha empaquetado con la extensión.

   :::image type="content" source="media/notebook-extension/notebook-launch-ads.png" alt-text="Comando Notebook":::

¡Enhorabuena! Ha creado la primera extensión de Jupyter Notebook y ya puede enviarla.

## <a name="publish-your-extension-to-the-marketplace"></a>Publicación de la extensión en Marketplace

El marketplace de extensiones de Azure Data Studio todavía no se ha implementado de forma completa. Para publicar, hospede la extensión VSIX en algún lugar (por ejemplo, una página de versión de GitHub) y envíe una solicitud de incorporación de cambios que actualice [este archivo JSON](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json) con la información de la extensión.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido a:
> [!div class="checklist"]
> - Creación de un proyecto de extensión
> - Instalar el generador de extensiones: crear la extensión de cuaderno
> - Creación de la extensión
> - Empaquetado de la extensión
> - Publicación de la extensión en Marketplace

Confiamos en que después de leer esto se sienta inspirado para compilar su propia extensión para Azure Data Studio.

Si tiene una idea, pero no está seguro de cómo empezar, abra una incidencia o envíe un Tweet al equipo: [azuredatastudio](https://twitter.com/azuredatastudio).

Siempre puede hacer referencia a la [guía de extensiones de Visual Studio Code](https://code.visualstudio.com/docs/extensions/overview) porque aborda todas las API y los patrones existentes.