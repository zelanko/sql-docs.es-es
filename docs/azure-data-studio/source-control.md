---
title: Control de código fuente
titleSuffix: Azure Data Studio
description: Obtenga información sobre cómo configurar el control de código fuente en Azure Data Studio
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: c278bcf6cff451396b3d677b203f207b68fd6dc5
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "67959288"
---
#  <a name="using-source-control-in-includename-sosincludesname-sos-shortmd"></a>Uso del control de código fuente en [!INCLUDE[name-sos](../includes/name-sos-short.md)]

[!INCLUDE[name-sos](../includes/name-sos-short.md)] admite Git para el control de código fuente o versiones.


## <a name="git-support-in-includename-sosincludesname-sos-shortmd"></a>Compatibilidad de Git en [!INCLUDE[name-sos](../includes/name-sos-short.md)]

[!INCLUDE[name-sos](../includes/name-sos-short.md)] se suministra con un administrador de control de código fuente (SCM) de Git, pero sigue siendo necesario [instalar Git (versión 2.0.0 o posterior)](https://git-scm.com/download) para que estas características estén disponibles. 



## <a name="open-an-existing-git-repository"></a>Apertura de un repositorio de Git existente

1. En el menú **Archivo**, seleccione **Abrir carpeta...**
2. Vaya a la carpeta que contiene los archivos a los que Git realiza un seguimiento y haga clic en **Seleccionar carpeta**. Aquí puede seleccionar las subcarpetas de su repositorio local.


## <a name="initialize-a-new-git-repository"></a>Inicialización de un nuevo repositorio de Git

1. Seleccione **Control de código fuente** y después seleccione el icono de Git.

   ![Inicio de Git del control de código fuente](media/source-control/source-control.png)

1. Escriba la ruta de acceso a la carpeta que quiera inicializar como un repositorio de Git y presione **Entrar**.

   ![Inicialización del repositorio de Git](media/source-control/initialize-git-repository.png)

## <a name="working-with-git-repositories"></a>Trabajo con repositorios de Git

[!INCLUDE[name-sos](../includes/name-sos-short.md)] hereda su implementación de Git de VS Code, pero actualmente no admite proveedores de SCM adicionales. Para obtener información detallada sobre cómo trabajar con Git después de abrir o inicializar un repositorio, consulte [Compatibilidad de Git en VS Code](https://code.visualstudio.com/docs/editor/versioncontrol#_git-support).


## <a name="additional-resources"></a>Recursos adicionales
- [Documentación de Git](https://git-scm.com/documentation)
