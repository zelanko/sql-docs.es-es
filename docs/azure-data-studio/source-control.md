---
title: Control en Azure Data Studio de código fuente | Microsoft Docs
description: Obtenga información sobre cómo configurar el control de código fuente en Azure Data Studio.
ms.custom: tools|sos
ms.date: 09/24/2018
ms.prod: sql
ms.technology: azure-data-studio
ms.reviewer: alayu; sstein
ms.topic: conceptual
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 956ead73c4fe28a045f5ff24280012ed32937f9c
ms.sourcegitcommit: 35e4c71bfbf2c330a9688f95de784ce9ca5d7547
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/16/2018
ms.locfileid: "49356316"
---
#  <a name="using-source-control-in-includename-sosincludesname-sos-shortmd"></a>Uso del control de código fuente en [!INCLUDE[name-sos](../includes/name-sos-short.md)]

[!INCLUDE[name-sos](../includes/name-sos-short.md)] es compatible con Git para control de versión/código fuente.


## <a name="git-support-in-includename-sosincludesname-sos-shortmd"></a>Compatibilidad con GIT en [!INCLUDE[name-sos](../includes/name-sos-short.md)]

[!INCLUDE[name-sos](../includes/name-sos-short.md)] se distribuye con un administrador de control de código fuente (SCM) de Git, pero aun así deberá [instale Git (versión 2.0.0 o posterior)](https://git-scm.com/download) antes de que estas características están disponibles. 



## <a name="open-an-existing-git-repository"></a>Abra un repositorio Git existente

1. En el **archivo** menú, seleccione **Abrir carpeta...**
2. Vaya a la carpeta que contiene los archivos de git realiza el seguimiento y haga clic en **seleccionar la carpeta**. Las subcarpetas en el repositorio local están en buen estadas para que seleccione aquí.


## <a name="initialize-a-new-git-repository"></a>Inicializar un nuevo repositorio git

1. Seleccione **Control de código fuente**, a continuación, seleccione el icono de git.

   ![Icono de git de control de código fuente](media/source-control/source-control.png)

1. Escriba la ruta de acceso a la carpeta que desea inicializar como un repositorio de Git y presione **ENTRAR**.

   ![inicializar repositorio Git](media/source-control/initialize-git-repository.png)

## <a name="working-with-git-repositories"></a>Trabajar con repositorios de Git

[!INCLUDE[name-sos](../includes/name-sos-short.md)] hereda su implementación de Git de VS Code, pero no se admite actualmente los proveedores SCM adicionales. Para obtener los detalles sobre cómo trabajar con Git después de abrir o inicialice un repositorio, consulte [compatibilidad con Git en VS Code](https://code.visualstudio.com/docs/editor/versioncontrol#_git-support).


## <a name="additional-resources"></a>Recursos adicionales
- [Documentación de GIT](https://git-scm.com/documentation)
