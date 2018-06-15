---
title: Las operaciones de SQL Studio (versión preliminar) usuario y la configuración de área de trabajo | Documentos de Microsoft
description: Cómo modificar la configuración de área de trabajo y las operaciones de SQL Studio usuario (vista previa).
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql
ms.reviewer: alayu; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: yualan
ms.author: alayu
manager: craigg
ms.openlocfilehash: 67f60d30693eeb60030f3a977ec1bcf5a1f98be1
ms.sourcegitcommit: 6fd8a193728abc0a00075f3e4766a7e2e2859139
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/17/2018
ms.locfileid: "34235142"
---
# <a name="user-and-workspace-settings"></a>Configuración de área de trabajo y de usuario

Es fácil de configurar [!INCLUDE[name-sos](../includes/name-sos-short.md)] a su gusto a través de configuración. Casi todas las partes de [!INCLUDE[name-sos](../includes/name-sos-short.md)]del editor, la interfaz de usuario y el comportamiento funcional tiene opciones puede modificar.

[!INCLUDE[name-sos](../includes/name-sos-short.md)] proporciona dos ámbitos diferentes para la configuración:

* **Usuario** estas opciones se aplican globalmente a cualquier instancia de [!INCLUDE[name-sos](../includes/name-sos-short.md)] abrir.
* **Área de trabajo** configuración de área de trabajo son configuraciones específicas de una carpeta en el equipo y sólo están disponibles cuando la carpeta se abre en la barra lateral de explorador. Opciones de configuración definidas en este ámbito de invalidan el ámbito del usuario.

## <a name="creating-user-and-workspace-settings"></a>Creación de usuario y la configuración de área de trabajo

El comando de menú **archivo** > **preferencias** > **configuración** (**código**  >  **Preferencias** > **configuración** en Mac) proporciona el punto de entrada para configurar el área de trabajo y usuario. Se le proporcionará una lista de configuración predeterminada. Copiar cualquier configuración que desea cambiar a la correspondiente `settings.json` archivo. Las pestañas de la derecha permiten cambiar rápidamente entre los archivos de configuración de área de trabajo y usuario.

También puede abrir la configuración de área de trabajo y usuario de la **comando paleta** (**Ctrl + Mayús + P**) con **preferencias: abra Configuración de usuario** y  **Preferencias: Abrir la configuración de área de trabajo** o use el método abreviado de teclado (**Ctrl +**).

En el ejemplo siguiente se deshabilita los números de línea en el editor y configura las líneas de código que se les aplica sangría automáticamente.

![Configuración de ejemplo](media/settings/sample-settings.png)

Cambios en la configuración se vuelven a cargar por [!INCLUDE[name-sos](../includes/name-sos-short.md)] después modificados `settings.json` archivo se guarda.

>**Nota:** configuración de área de trabajo es útiles para compartir la configuración específica del proyecto en un equipo.

## <a name="settings-file-locations"></a>Ubicaciones de archivos de configuración

Dependiendo de la plataforma, el archivo de configuración de usuario se encuentra aquí:

* **Windows** `%APPDATA%\sqlops\User\settings.json`
* **Mac** `$HOME/Library/Application Support/sqlops/User/settings.json`
* **Linux** `$HOME/.config/sqlops/User/settings.json`

El archivo de configuración de área de trabajo se encuentra en la `.[!INCLUDE[name-sos](../includes/name-sos-short.md)]` carpeta del proyecto.

## <a name="hot-exit"></a>Salida activa

Operaciones de SQL Studio recordará los cambios no guardados a los archivos cuando se cierra de forma predeterminada. Esto es igual que la característica de salida activas en el código de Visual Studio.

De forma predeterminada, la salida activa está desactivada. Habilitar activa salida mediante la edición de la `files.hotExit` configuración. Para obtener más información, consulte [salida activa (en la documentación de Visual Studio Code)](https://code.visualstudio.com/docs/editor/codebasics#_hot-exit).


## <a name="tab-color"></a>Color de etiqueta

Para simplificar la identificación de las conexiones que se trabaja con, pestañas abiertas en el editor pueden tener sus colores establecidos para que coincida con el color del grupo de servidores al que pertenece la conexión. De forma predeterminada, los colores de la ficha están desactivadas de forma predeterminada. Habilitar colores de pestaña editando el `sql.tabColorMode` configuración.

## <a name="additional-resources"></a>Recursos adicionales

Dado que [!INCLUDE[name-sos](../includes/name-sos-short.md)] hereda su configuración de área de trabajo y usuario funcionalidad desde el código de Visual Studio, información detallada acerca de la configuración se encuentra en la [configuración de Visual Studio Code](https://code.visualstudio.com/docs/getstarted/settings) artículo.
