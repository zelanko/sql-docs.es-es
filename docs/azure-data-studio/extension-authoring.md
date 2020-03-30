---
title: Creación de extensiones
titleSuffix: Azure Data Studio
description: Más información sobre cómo crear extensiones y agregarlas a Azure Data Studio
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: d0c43df8b24a33f3763dc5ff3a80e989b9b85038
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "67959602"
---
# <a name="extend-the-functionality-by-creating-azure-data-studio-extensions"></a>Extensión de la funcionalidad mediante la creación de extensiones de Azure Data Studio

Las extensiones de [!INCLUDE[name-sos](../includes/name-sos-short.md)] proporcionan una manera sencilla de agregar más funcionalidad a la instalación base de [!INCLUDE[name-sos](../includes/name-sos-short.md)].

Las extensiones las proporciona el equipo de Azure Data Studio (Microsoft), así como la comunidad (los usuarios).


## <a name="author-an-extension"></a>Creación de una extensión

Si está interesado en las extensiones de Azure Data Studio, puede crear su propia extensión y publicarla en la galería de extensiones.

**Escritura de una extensión**

***Requisitos previos***

Para desarrollar una extensión ha de tener Node.js instalado y disponible en la variable $PATH. Node.js incluye npm, el administrador de paquetes de Node.js, que se usará para instalar el generador de extensiones.

Para iniciar la nueva extensión, puede usar el generador de extensiones de Azure Data Studio. El [generador de extensiones](https://www.npmjs.com/package/generator-azuredatastudio) Yeoman facilita enormemente la creación de proyectos de extensión sencillos. Para iniciar el generador, escriba lo siguiente en un símbolo del sistema:

`npm install -g yo generator-azuredatastudio`

`yo azuredatastudio`


**Referencias de extensibilidad**

Para obtener información sobre la extensibilidad de Azure Data Studio, consulte el artículo sobre [introducción a la extensibilidad](extensibility.md). También puede ver ejemplos de uso de la API en [ejemplos](https://github.com/Microsoft/azuredatastudio/tree/master/samples) existentes.


## <a name="debug-an-extension"></a>Depuración de una extensión

Puede depurar la nueva extensión mediante la extensión [Debug de Azure Data Studio](https://github.com/kevcunnane/sqlops-debug) de Visual Studio Code.

Pasos
- Abra la extensión con [Visual Studio Code](https://code.visualstudio.com/).
- Instale la extensión Debug de Azure Data Studio.
- Presione **F5** o hacer clic en el icono de depuración y en **Iniciar**.
- Se inicia una nueva instancia de Azure Data Studio en un modo especial (Host de desarrollo de la extensión) y esta nueva instancia tiene ahora en cuenta la extensión.


## <a name="create-an-extension-package"></a>Creación de un paquete de extensión

Después de escribir la extensión, ha de crear un paquete VSIX para poder instalarlo en Azure Data Studio. Puede usar [vsce](https://github.com/Microsoft/vscode-vsce) para crear el paquete VSIX.

`npm install -g vsce`

`vsce package`


## <a name="publish-an-extension"></a>Publicación de una extensión

Para publicar la nueva extensión en Azure Data Studio:

1. Agregue la extensión a https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json.
2. Actualmente no tenemos soporte para hospedar extensiones de terceros, por lo que en lugar de descargar la extensión, Azure Data Studio tiene la opción de ir a una página de descarga. Para establecer una página de descarga para la extensión, establezca el valor del recurso "Microsoft.AzureDataStudio.DownloadPage".
3. Cree una solicitud de incorporación de cambios en la rama de versión/extensiones.
4. Envíe una solicitud de revisión al equipo.

La extensión se revisará y se agregará a la galería de extensiones.

**Publicación de actualizaciones de extensiones** El proceso de publicación de actualizaciones es similar al de publicación de una extensión. Asegúrese de que la versión esté actualizada en package.json.
