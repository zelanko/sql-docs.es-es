---
title: Creación de extensiones
description: Puede agregar funcionalidad a Azure Data Studio con una extensión. Obtenga información sobre cómo crear una y publicarla en la galería de extensiones.
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu, maghan, sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: bd2a20857c8f16ea2b2d71ebfcb620bcea3f0190
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778424"
---
# <a name="extend-the-functionality-by-creating-azure-data-studio-extensions"></a>Extensión de la funcionalidad mediante la creación de extensiones de Azure Data Studio

Las extensiones de Azure Data Studio proporcionan una manera sencilla de agregar más funcionalidad a la instalación base de Azure Data Studio.

Las extensiones las proporciona el equipo de Azure Data Studio (Microsoft), así como la comunidad (los usuarios).


## <a name="author-an-extension"></a>Creación de una extensión

Si está interesado en las extensiones de Azure Data Studio, puede crear su propia extensión y publicarla en la galería de extensiones.

**Escritura de una extensión**

***Requisitos previos***

Para desarrollar una extensión ha de tener [Node.js](https://nodejs.org/) instalado y disponible en `$PATH`. Node.js incluye npm, el administrador de paquetes de Node.js, que se usará para instalar el generador de extensiones.

Para crear la extensión, puede usar el generador de extensiones de Azure Data Studio. El [generador de extensiones](https://www.npmjs.com/package/generator-azuredatastudio) de Yeoman es un punto de partida beneficioso para los proyectos de extensión. Para iniciar el generador, escriba lo siguiente en un símbolo del sistema:

```
npm install -g yo generator-azuredatastudio # Install the generator
yo azuredatastudio
```

Para obtener instrucciones detalladas sobre cómo empezar a usar la plantilla de extensiones, consulte [Creación de una extensión](./tutorial-create-extension.md?view=sql-server-ver15), que le guía durante la creación de una extensión de distribución de teclado.

**Referencias de extensibilidad**

Para obtener información sobre la extensibilidad de Azure Data Studio, consulte el artículo sobre [introducción a la extensibilidad](extensibility.md). También puede ver ejemplos de uso de la API en [ejemplos](https://github.com/Microsoft/azuredatastudio/tree/main/samples) existentes.


## <a name="debug-an-extension"></a>Depuración de una extensión

Puede depurar la nueva extensión mediante la extensión [Debug de Azure Data Studio](https://github.com/kevcunnane/sqlops-debug) de Visual Studio Code.

Pasos
1. Abra la extensión con [Visual Studio Code](https://code.visualstudio.com/).
1. Instale la extensión Debug de Azure Data Studio.
1. Presione **F5** o hacer clic en el icono de depuración y en **Iniciar**.
1. Se inicia una nueva instancia de Azure Data Studio en un modo especial (Host de desarrollo de la extensión) y esta nueva instancia tiene ahora en cuenta la extensión.


## <a name="create-an-extension-package"></a>Creación de un paquete de extensión

Después de escribir la extensión, ha de crear un paquete VSIX para poder instalarlo en Azure Data Studio. Puede usar [vsce](https://github.com/Microsoft/vscode-vsce) (extensiones de Visual Studio Code) para crear el paquete VSIX. 

```
npm install -g vsce
cd myExtensionName
vsce package
# The myExtensionName.vsix file has now been generated
```

Con un paquete VSIX, puede compartir la extensión de forma local y privada si comparte el archivo `.vsix` y usa el comando **Extensiones: Instalar desde archivo VSIX** de la paleta de comandos con el fin de instalar la extensión en Azure Data Studio.


## <a name="publish-an-extension"></a>Publicación de una extensión

Para publicar la nueva extensión en Azure Data Studio:

1. Agregue la extensión a https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json.
2. Actualmente no tenemos soporte para hospedar extensiones de terceros, por lo que en lugar de descargar la extensión, Azure Data Studio tiene la opción de ir a una página de descarga. Para establecer una página de descarga para la extensión, establezca el valor del recurso "Microsoft.AzureDataStudio.DownloadPage".
3. Cree una solicitud de incorporación de cambios en la rama de versión/extensiones.
4. Envíe una solicitud de revisión al equipo.

La extensión se revisará y se agregará a la galería de extensiones.

**Publicación de actualizaciones de extensión**

El proceso de publicación de actualizaciones es similar al de publicación de una extensión. Asegúrese de que la versión esté actualizada en package.json.