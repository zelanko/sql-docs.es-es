---
title: Crear extensiones para Azure Data Studio | Microsoft Docs
description: Agregar extensiones a Azure Data Studio
ms.custom: tools|sos
ms.date: 09/24/2018
ms.reviewer: alayu; sstein
ms.prod: sql
ms.prod_service: sql-tools
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8935d641c8c3fa6da58b5f7c2d8b5560664a6486
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "48039155"
---
# <a name="extend-the-functionality-of-includename-sosincludesname-sos-shortmd"></a>Extender la funcionalidad de [!INCLUDE[name-sos](../includes/name-sos-short.md)]

Las extensiones en [!INCLUDE[name-sos](../includes/name-sos-short.md)] proporcionan una manera fácil de agregar más funcionalidad a la base de [!INCLUDE[name-sos](../includes/name-sos-short.md)] instalación.

Las extensiones son proporcionadas por el equipo de Azure Data Studio (Microsoft), así como la Comunidad parte 3ª (usted).


## <a name="author-an-extension"></a>Crear una extensión

Si está interesado en la extensión de Azure Data Studio, puede crear su propia extensión y publicarlo en la Galería de extensiones.

**Escribir una extensión**

***Requisitos previos***

Para desarrollar una extensión necesita Node.js instalado y disponible en la $PATH. Node.js incluye npm, el Administrador de paquetes de Node.js que se usará para instalar el generador de extensión.

Para iniciar la nueva extensión, puede usar el generador de Studio extensión de datos de Azure. El Yeoman [generador extensión](https://www.npmjs.com/package/generator-sqlops) facilita enormemente la creación de proyectos de extensión simple. Para iniciar el generador, escriba lo siguiente en un símbolo del sistema:

`npm install -g yo generator-sqlops`

`yo sqlops`


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
