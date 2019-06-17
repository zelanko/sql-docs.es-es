---
title: Crear extensiones
titleSuffix: Azure Data Studio
description: Obtenga información sobre cómo crear y agregar extensiones a Azure Data Studio
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 7628634ded2b3b8245e69d3f3697864e0982c850
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66800278"
---
# <a name="extend-the-functionality-by-creating-azure-data-studio-extensions"></a>Ampliar la funcionalidad mediante la creación de extensiones de Azure Data Studio

Las extensiones en [!INCLUDE[name-sos](../includes/name-sos-short.md)] proporcionan una manera fácil de agregar más funcionalidad a la base de [!INCLUDE[name-sos](../includes/name-sos-short.md)] instalación.

Las extensiones son proporcionadas por el equipo de Azure Data Studio (Microsoft), así como la Comunidad parte 3ª (usted).


## <a name="author-an-extension"></a>Crear una extensión

Si está interesado en la extensión de Azure Data Studio, puede crear su propia extensión y publicarlo en la Galería de extensiones.

**Escribir una extensión**

***Requisitos previos***

Para desarrollar una extensión necesita Node.js instalado y disponible en la $PATH. Node.js incluye npm, el Administrador de paquetes de Node.js que se usará para instalar el generador de extensión.

Para iniciar la nueva extensión, puede usar el generador de Studio extensión de datos de Azure. El Yeoman [generador extensión](https://www.npmjs.com/package/generator-azuredatastudio) facilita enormemente la creación de proyectos de extensión simple. Para iniciar el generador, escriba lo siguiente en un símbolo del sistema:

`npm install -g yo generator-azuredatastudio`

`yo azuredatastudio`


**Referencias de extensibilidad**

Para más información sobre Azure Data Studio extensibilidad consulte [información general sobre extensibilidad](extensibility.md). También puede ver ejemplos de cómo usar la API existente [ejemplos](https://github.com/Microsoft/azuredatastudio/tree/master/samples).


## <a name="debug-an-extension"></a>Depurar una extensión

Puede depurar la nueva extensión con la extensión de Visual Studio Code [Azure datos Studio depurar](https://github.com/kevcunnane/sqlops-debug).

Pasos
- Abra la extensión con [Visual Studio Code](https://code.visualstudio.com/)
- Instalar extensión Studio depurar de datos de Azure
- Presione **F5** o haga clic en el icono de depuración y haga clic en **iniciar**.
- Se inicia una nueva instancia de Azure Data Studio en un modo especial (Host de desarrollo de extensión) y ahora reconoce esta nueva instancia de la extensión.


## <a name="create-an-extension-package"></a>Crear un paquete de extensión

Después de escribir la extensión, deberá crear un paquete VSIX para poder instalarlo en Azure Data Studio. Puede usar [vsce](https://github.com/Microsoft/vscode-vsce) para crear el paquete VSIX.

`npm install -g vsce`

`vsce package`


## <a name="publish-an-extension"></a>Publicar una extensión

Para publicar la nueva extensión a Azure Data Studio:

1. Agregar la extensión https://github.com/Microsoft/azuredatastudio/blob/release/extensions/extensionsGallery.json
2. Actualmente no tenemos compatibilidad para las extensiones de terceros de host, por lo que en lugar de descargar la extensión, Azure Data Studio tiene la opción para ir a una página de descarga. Para establecer una página de descarga para la extensión, establezca el valor del activo "Microsoft.AzureDataStudio.DownloadPage".
3. Cree un PR en la rama de versión/extensiones.
4. Enviar una solicitud de revisión para el equipo.

La extensión se revisan y se agregará a la Galería de extensiones.

**Publicar actualizaciones de extensión** el proceso para publicar actualizaciones es similar a la publicación de la extensión. Asegúrese de que se actualiza la versión en package.json
