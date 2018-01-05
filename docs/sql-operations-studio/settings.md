---
title: "Las operaciones de SQL Studio (versión preliminar) usuario y la configuración de área de trabajo | Documentos de Microsoft"
description: "Cómo modificar la configuración de área de trabajo y las operaciones de SQL Studio usuario (vista previa)."
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql-non-specified
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: 
ms.topic: article
author: yualan
ms.author: alayu
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2edea069c05e7ac0316042250f336f1a8c455af0
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="user-and-workspace-settings"></a>Configuración de área de trabajo y de usuario

Es fácil de configurar [!INCLUDE[name-sos](../includes/name-sos-short.md)] a su gusto a través de configuración. Casi todas las partes de [!INCLUDE[name-sos](../includes/name-sos-short.md)]del editor, la interfaz de usuario y el comportamiento funcional tiene opciones puede modificar.

[!INCLUDE[name-sos](../includes/name-sos-short.md)]proporciona dos ámbitos diferentes para la configuración:

* **Usuario** estas opciones se aplican globalmente a cualquier instancia de [!INCLUDE[name-sos](../includes/name-sos-short.md)] abrir.
* **Área de trabajo** configuración de área de trabajo son configuraciones específicas de una carpeta en el equipo y sólo están disponibles cuando la carpeta se abre en la barra lateral de explorador. Opciones de configuración definidas en este ámbito de invalidan el ámbito del usuario.

## <a name="creating-user-and-workspace-settings"></a>Creación de usuario y la configuración de área de trabajo

El comando de menú **archivo** > **preferencias** > **configuración** (**código**  >  **Preferencias** > **configuración** en Mac) proporciona el punto de entrada para configurar el área de trabajo y usuario. Se le proporcionará una lista de configuración predeterminada. Copiar cualquier configuración que desea cambiar a la correspondiente `settings.json` archivo. Las pestañas de la derecha permiten cambiar rápidamente entre los archivos de configuración de área de trabajo y usuario.

También puede abrir la configuración de área de trabajo y usuario de la **comando paleta** (**Ctrl + Mayús + P**) con **preferencias: abra Configuración de usuario** y  **Preferencias: Abrir la configuración de área de trabajo** o use el método abreviado de teclado (**Ctrl +**).

En el ejemplo siguiente se deshabilita los números de línea en el editor y configura las líneas de ajuste automáticamente basándose en el tamaño del editor de texto.

![Configuración de ejemplo](media/settings/sample-settings.png)

Cambios en la configuración se vuelven a cargar por [!INCLUDE[name-sos](../includes/name-sos-short.md)] después modificados `settings.json` archivo se guarda.

>**Nota:** configuración de área de trabajo es útiles para compartir la configuración específica del proyecto en un equipo.

## <a name="settings-file-locations"></a>Ubicaciones de archivos de configuración

Dependiendo de la plataforma, el archivo de configuración de usuario se encuentra aquí:

* **Windows**`%APPDATA%\sqlops\User\settings.json`
* **Mac**`$HOME/Library/Application Support/sqlops/User/settings.json`
* **Linux**`$HOME/.config/sqlops/User/settings.json`

El archivo de configuración de área de trabajo se encuentra en la `.[!INCLUDE[name-sos](../includes/name-sos-short.md)]` carpeta del proyecto.


## <a name="additional-resources"></a>Recursos adicionales

Dado que [!INCLUDE[name-sos](../includes/name-sos-short.md)] hereda su configuración de área de trabajo y usuario funcionalidad desde el código de Visual Studio, información detallada acerca de la configuración se encuentra en la [configuración de Visual Studio Code](https://code.visualstudio.com/docs/getstarted/settings) artículo.