---
title: Usuario y la configuración de área de trabajo
titleSuffix: Azure Data Studio
description: Cómo personalizar Azure Data Studio mediante la modificación de usuario y la configuración de área de trabajo.
ms.custom: seodec18
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: yualan
ms.author: alayu
ms.openlocfilehash: a874aaf9ec136ff9ea27cbeaa92011a07f3718c7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959272"
---
# <a name="modify-user-and-workspace-settings"></a>Modificar la configuración de área de trabajo y usuario

Es fácil de configurar [!INCLUDE[name-sos](../includes/name-sos-short.md)] a su gusto a través de configuración. Casi todas las partes de [!INCLUDE[name-sos](../includes/name-sos-short.md)]del editor, la interfaz de usuario y comportamiento funcional tiene opciones puede modificar.

[!INCLUDE[name-sos](../includes/name-sos-short.md)] proporciona dos ámbitos diferentes para la configuración:

* **Usuario** esta configuración se aplica globalmente a cualquier instancia de [!INCLUDE[name-sos](../includes/name-sos-short.md)] abrir.
* **Área de trabajo** configuración de área de trabajo son valores específicos de una carpeta en el equipo y solo están disponibles cuando la carpeta se abre en la barra lateral de explorador. Configuración definida en este ámbito invalida el ámbito del usuario.

## <a name="creating-user-and-workspace-settings"></a>Creación de usuario y la configuración de área de trabajo

El comando de menú **archivo** > **preferencias** > **configuración** (**código**  >  **Preferencias** > **configuración** en Mac) proporciona el punto de entrada para configurar la configuración de usuario y el área de trabajo. Se proporcionan con una lista de la configuración predeterminada. Copiar cualquier configuración que desea cambiar a la correspondiente `settings.json` archivo. Las pestañas de la derecha le permite alternar rápidamente entre los archivos de configuración de usuario y el área de trabajo.

También puede abrir la configuración de usuario y del área de trabajo desde el **paleta de comandos** (**Ctrl + Mayús + P**) con **preferencias: Abrir configuración de usuario** y **preferencias: Abrir configuración de área de trabajo** o use el método abreviado de teclado (**Ctrl +,** ).

El siguiente ejemplo deshabilita los números de línea en el editor y configura las líneas de código que se les aplica sangría automáticamente.

![Configuración de ejemplo](media/settings/sample-settings.png)

Se vuelven a cargar los cambios de configuración por [!INCLUDE[name-sos](../includes/name-sos-short.md)] después modificado `settings.json` se guarda el archivo.

>**Nota:** Configuración de área de trabajo es útiles para compartir la configuración específica del proyecto a través de un equipo.

## <a name="settings-file-locations"></a>Ubicaciones de archivo de configuración

Dependiendo de la plataforma, el archivo de configuración de usuario se encuentra aquí:

* **Windows** `%APPDATA%\azuredatastudio\User\settings.json`
* **Mac** `$HOME/Library/Application Support/azuredatastudio/User/settings.json`
* **Linux** `$HOME/.config/azuredatastudio/User/settings.json`

El archivo de configuración de área de trabajo se encuentra en la `.[!INCLUDE[name-sos](../includes/name-sos-short.md)]` carpeta del proyecto.

## <a name="hot-exit"></a>Salida de acceso frecuente

Azure Data Studio recuerda los cambios no guardados en archivos cuando se cierra de forma predeterminada. Esto es lo mismo que la característica hot salir en Visual Studio Code.

De forma predeterminada, la salida activo está desactivada. Habilitar salida hot editando el `files.hotExit` configuración. Para obtener más información, consulte [activo de salida (en la documentación de Visual Studio Code)](https://code.visualstudio.com/docs/editor/codebasics#_hot-exit).


## <a name="tab-color"></a>Color de etiqueta

Para simplificar la identificación de las conexiones que se trabaja con, las pestañas abiertas en el editor pueden tener sus colores establecidos para que coincida con el color del grupo de servidores al que pertenece la conexión. De forma predeterminada, los colores de pestaña están desactivados de forma predeterminada. Habilitar los colores de pestaña editando el `sql.tabColorMode` configuración.

## <a name="additional-resources"></a>Recursos adicionales

Dado que [!INCLUDE[name-sos](../includes/name-sos-short.md)] hereda su configuración de usuario y el área de trabajo en la funcionalidad de Visual Studio Code, información detallada acerca de la configuración es la [valores para Visual Studio Code](https://code.visualstudio.com/docs/getstarted/settings) artículo.
