---
title: Origen de control en las operaciones de SQL Studio (versión preliminar) | Documentos de Microsoft
description: Obtenga información acerca de cómo configurar el control de código fuente en las operaciones de SQL Studio (versión preliminar).
ms.custom: tools|sos
ms.date: 11/15/2017
ms.prod: sql
ms.reviewer: alayu; erickang; sstein
ms.suite: sql
ms.prod_service: sql-tools
ms.component: sos
ms.tgt_pltfrm: ''
ms.topic: article
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 73fec13868004469b02f3117b9b8d70e1ec26ff3
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
#  <a name="using-source-control-in-includename-sosincludesname-sos-shortmd"></a>Uso de control de código fuente en [!INCLUDE[name-sos](../includes/name-sos-short.md)]

[!INCLUDE[name-sos](../includes/name-sos-short.md)] es compatible con Git para el control de versiones u origen.


## <a name="git-support-in-includename-sosincludesname-sos-shortmd"></a>Compatibilidad de GIT en [!INCLUDE[name-sos](../includes/name-sos-short.md)]

[!INCLUDE[name-sos](../includes/name-sos-short.md)] se suministra con un administrador de control de código fuente Git (SCM), pero aún necesite [instale Git (versión 2.0.0 o posterior)](https://git-scm.com/download) antes de que estas características están disponibles. 



## <a name="open-an-existing-git-repository"></a>Abra un repositorio de Git existente

1. En el **archivo** menú, seleccione **Abrir carpeta...**
2. Vaya a la carpeta que contiene los archivos que se hace un seguimiento mediante git y haga clic en **seleccionar la carpeta**. Las subcarpetas en el repositorio local son correctos seleccionar aquí.


## <a name="initialize-a-new-git-repository"></a>Inicializar un nuevo repositorio git

1. Seleccione **Control de código fuente**, a continuación, seleccione el icono de git.

   ![Icono de git de control de código fuente](media/source-control/source-control.png)

1. Escriba la ruta de acceso a la carpeta que desea inicializar como un repositorio Git y presione **ENTRAR**.

   ![inicializar el repositorio de Git](media/source-control/initialize-git-repository.png)

## <a name="working-with-git-repositories"></a>Trabajar con repositorios Git

[!INCLUDE[name-sos](../includes/name-sos-short.md)] hereda su implementación de Git desde el código de VS, pero no admite actualmente los proveedores SCM adicionales. Para obtener los detalles sobre cómo trabajar con Git después de abrir o inicializar un repositorio, consulte [compatibilidad de Git en VS Code](https://code.visualstudio.com/docs/editor/versioncontrol#_git-support).


## <a name="additional-resources"></a>Recursos adicionales
- [Documentación de GIT](https://git-scm.com/documentation)
