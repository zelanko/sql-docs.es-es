---
title: Creación de una extensión de libro de Jupyter
description: Obtenga información sobre cómo empaquetar un libro de Jupyter en una extensión mediante el generador de extensiones
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: how-to
author: yualan
ms.author: alayu
ms.reviewer: alayu, maghan
ms.custom: ''
ms.date: 08/28/2020
ms.openlocfilehash: af6cb013109d5d871c709f72cf5a564ae69940cb
ms.sourcegitcommit: b6ee0d434b3e42384b5d94f1585731fd7d0eff6f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/02/2020
ms.locfileid: "89288177"
---
# <a name="create-a-jupyter-book-extension"></a>Creación de una extensión de libro de Jupyter

En este tutorial se muestra cómo crear una extensión de libro de Jupyter de Azure Data Studio. La extensión envía un libro de Jupyter de ejemplo que se puede abrir y ejecutar en Azure Data Studio. 

Durante este tutorial aprenderá a realizar lo siguiente:
> [!div class="checklist"]
> - Creación de un proyecto de extensión
> - Instalación del generador de extensiones
> - Crear la extensión de libro de Jupyter
> - Ejecutar la extensión
> - Empaquetado de la extensión
> - Publicación de la extensión en Marketplace

## <a name="apis-used"></a>API utilizadas

- `bookTreeView.openBook`

### <a name="extension-use-cases"></a>Casos de uso de la extensión

Hay varias razones para crear una extensión de libro de Jupyter:

- Compartir documentación interactiva y organizada en secciones
- Compartir un libro completo (similar a un libro electrónico, pero distribuido a través de Azure Data Studio)
- Crear versiones y realizar el seguimiento de las actualizaciones del libro de Jupyter

La diferencia principal entre un libro de Jupyter y una extensión de cuaderno es que un libro de Jupyter proporciona organización. Se pueden dividir decenas de cuadernos en capítulos diferentes de un libro, pero la extensión de cuadernos está diseñada para enviar una cantidad reducida de cuadernos individuales.

## <a name="prerequisites"></a>Prerrequisitos

Azure Data Studio se basa en el mismo marco que Visual Studio Code, por lo que las extensiones para Azure Data Studio se crean con Visual Studio Code. Para comenzar, necesitará los siguientes componentes:

- [Node.js](https://nodejs.org) instalado y disponible en su `$PATH`. Node.js incluye [npm](https://www.npmjs.com/), el administrador de paquetes de Node.js, que se usa para instalar el generador de extensiones.
- [Visual Studio Code](https://code.visualstudio.com) para realizar cambios en la extensión y depurarla.
- Asegúrese de que `azuredatastudio` está en su ruta de acceso. En el caso de Windows, asegúrese de elegir la opción `Add to Path` de setup.exe. En Mac o Linux, ejecute la opción de *instalación del comando "azuredatastudio" de PATH*.

## <a name="install-the-extension-generator"></a>Instalación del generador de extensiones

Para simplificar el proceso de creación de extensiones, hemos compilado [un generador de extensiones](https://www.npmjs.com/package/generator-azuredatastudio) con Yeoman. Para instalarlo, ejecute el comando siguiente desde el símbolo del sistema:

```console
`npm install -g yo generator-azuredatastudio`
```

## <a name="create-your-extension"></a>Creación de la extensión

Para crear una extensión:

1. Inicie el generador de extensiones con el siguiente comando:

   `yo azuredatastudio`

2. Elija **Nuevo libro de Jupyter** en la lista de tipos de extensiones:

   :::image type="content" source="media/jupyter-book-extension/jupyter-book-extension-generator.png" alt-text="Generador de extensiones":::

3. Siga los pasos para rellenar el nombre de la extensión (para este tutorial, use **Libro de prueba**), un nombre de publicador (para este tutorial, use **Microsoft**) y agregue una descripción.

Puede elegir entre proporcionar un libro de Jupyter existente, usar un libro de ejemplo proporcionado, o bien trabajar para crear uno. Las tres opciones se muestran a continuación.

### <a name="providing-an-existing-book"></a>Proporcionar un libro existente

Si quiere enviar un libro que ya ha creado, proporcione la ruta de acceso de archivo absoluta a la carpeta en la que reside el contenido del libro. Después, estará listo para continuar y obtener información sobre la extensión y cómo enviarla.

:::image type="content" source="media/jupyter-book-extension/jupyter-book-existing-book.png" alt-text="Libro existente":::

### <a name="using-the-sample-book"></a>Uso del libro de ejemplo

Si no tiene un libro o cuadernos existentes, puede usar el ejemplo proporcionado en el generador.

:::image type="content" source="media/jupyter-book-extension/jupyter-book-sample-path.png" alt-text="Libro de Jupyter de ejemplo":::

El libro de ejemplo muestra el aspecto de un libro de Jupyter sencillo. Si quiere obtener información sobre cómo personalizar un libro de Jupyter, vea la sección siguiente sobre cómo crear un libro con cuadernos existentes.

### <a name="creating-a-new-book"></a>Creación de un libro

Si tiene cuadernos que le gustaría empaquetar en un libro de Jupyter, puede hacerlo. El generador le preguntará si quiere incluir capítulos en el libro y, en ese caso, cuántos y sus títulos. Puede ver el aspecto del proceso de selección a continuación. Use la barra espaciadora para seleccionar los cuadernos que quiera colocar en cada capítulo.

:::image type="content" source="media/jupyter-book-extension/jupyter-book-create-book.png" alt-text="Creación del libro de Jupyter":::

Al completar los pasos anteriores, se crea una carpeta con el nuevo libro de Jupyter. Abra la carpeta en Visual Studio Code y estará listo para enviar la extensión de libro de Jupyter.

## <a name="understanding-your-extension"></a>Descripción de la extensión

Este es el aspecto que debe tener el proyecto:

   :::image type="content" source="media/jupyter-book-extension/jupyter-book-file-structure-generator.png" alt-text="Estructura de los archivos de la extensión":::

`vsc-extension-quickstart.md` proporciona una referencia de los archivos importantes. En `README.md` puede proporcionar documentación para la nueva extensión. Observe los archivos `package.json`, `jupyter-book.ts`, `content` y `toc.yml`. La carpeta `content` contiene todos los archivos Markdown o de cuaderno. `toc.yml` estructura el libro de Jupyter y se genera automáticamente si ha optado por crear un libro de Jupyter personalizado a través del Generador de extensiones.

Si ha creado un libro con el generador y ha optado por incluir capítulos, la estructura de carpetas tendría un aspecto ligeramente distinto. En lugar de que los archivos Markdown y de Jupyter Notebook estén en la carpeta `content`, habría subcarpetas correspondientes a los títulos elegidos para los capítulos. 

Si hay archivos o carpetas que no quiere publicar, puede incluir sus nombres en el archivo `.vscodeignore`.

Ahora se examinará `jupyter-book.ts` para comprender lo que hace la extensión recién creada.

```javascript
// This function is called when you run the command `Launch Book: Test Book` from
// command palette in Azure Data Studio. If you would like any additional functionality
// to occur when you launch the book, add to the activate function.
export function activate(context: vscode.ExtensionContext) {
    context.subscriptions.push(vscode.commands.registerCommand('launchBook.test-book', () => {
        processNotebooks();
    }));

    // Add other code here if you want to register another command
}
```

La función `activate` es la acción principal de la extensión. Los comandos que quiera registrar deben aparecer dentro de la función `activate`, similar al comando `launchBook.test-book`. Dentro de la función `processNotebooks`, se encuentra la carpeta de extensión que contiene el libro de Jupyter y se llama a `bookTreeView.openBook` con la carpeta de la extensión como parámetro. 

El archivo `package.json` también desempeña un papel importante en el registro del comando de la extensión:

```json
"activationEvents": [
        "onCommand:launchBook.test-book"
    ],
    "main": "./out/notebook.js",
    "contributes": {
        "commands": [
            {
                "command": "launchBook.test-book",
                "title": "Launch Book: Test Book"
            }
        ]
    }
```

El evento de activación, `onCommand`, desencadena la función que se ha registrado al invocar el comando. Hay otros eventos de activación posibles para tareas de personalización adicionales. Para obtener más información, vea [Eventos de activación](https://code.visualstudio.com/api/references/activation-events).

## <a name="package-your-extension"></a>Empaquetado de la extensión

Para compartirla con otros usuarios, tendrá que empaquetar la extensión en un único archivo. Este se puede publicar en el marketplace de extensiones de Azure Data Studio, o bien compartir entre el equipo o la comunidad. Para ello, debe instalar otro paquete npm desde la línea de comandos:

```console
`npm install -g vsce`
```

Edite `README.md` como prefiera, vaya hasta el directorio base de la extensión y ejecute `vsce package`. Opcionalmente, puede vincular un repositorio con la extensión o continuar sin ninguno. Para agregar uno, agregue una línea similar al archivo `package.json`.

```json
"repository": {
    "type": "git",
    "url": "https://github.com/laurajjiang/testbook.git"
}
```

Después de agregar estas líneas, se crea el archivo test-book-0.0.1.vsix, listo para instalarlo en Azure Data Studio.

## <a name="run-your-extension"></a>Ejecución de la extensión

Para ejecutar y probar la extensión, abra Azure Data Studio y abra la paleta de comandos (`Ctrl + Shift + P`). Busque el comando **Extensiones: Instalar desde VSIX** y navegue hasta la carpeta que contiene la nueva extensión. Ahora debería aparecer en el panel de extensiones de Azure Data Studio.

   :::image type="content" source="media/jupyter-book-extension/install-vsix.png" alt-text="Instalación de VSIX":::

Vuelva a abrir la paleta de comandos y busque el comando que ha registrado, **Iniciar libro: cuaderno de prueba**. Al ejecutarlo, debe abrir el libro de Jupyter que ha empaquetado con la extensión.

   :::image type="content" source="media/jupyter-book-extension/jupyter-book-launch-ads.png" alt-text="Comando Notebook":::

¡Enhorabuena! Ha creado la primera extensión de libro de Jupyter y ya puede enviarla. Para obtener más información sobre los libros de Jupyter, vea [Libros con Jupyter](https://jupyterbook.org/intro.html).

## <a name="publish-your-extension-to-the-marketplace"></a>Publicación de la extensión en marketplace

El marketplace de extensiones de Azure Data Studio todavía no se ha implementado de forma completa. Para publicar, hospede la extensión VSIX en algún lugar (por ejemplo, una página de versión de GitHub) y envíe una solicitud de incorporación de cambios que actualice [este archivo JSON](https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json) con la información de la extensión.

## <a name="next-steps"></a>Pasos siguientes

En este tutorial, ha aprendido a:
> [!div class="checklist"]
> - Creación de un proyecto de extensión
> - Instalación del generador de extensiones
> - Crear la extensión de libro de Jupyter
> - Empaquetado de la extensión
> - Publicación de la extensión en Marketplace

Esperamos que, después de leer esto, tendrá ideas sobre libros de Jupyter que le gustaría compartir en la comunidad de Azure Data Studio. 

Si tiene una idea, pero no está seguro de cómo empezar, abra una incidencia o envíe un tuit al equipo: [azuredatastudio](https://twitter.com/azuredatastudio).

Siempre puede hacer referencia a la [guía de extensiones de Visual Studio Code](https://code.visualstudio.com/docs/extensions/overview) porque aborda todas las API y los patrones existentes.
