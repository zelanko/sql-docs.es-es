---
title: 'Paso 1: Creación de carpetas de trabajo y variables de entorno | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 45091ba2-ea3d-4399-9814-489d812b42cc
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b58da11d973d169a0372e59c7e8d7e174e3cf789
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/22/2019
ms.locfileid: "58392133"
---
# <a name="step-1-creating-working-folders-and-environment-variables"></a>Paso 1: Crear carpetas de trabajo y variables de entorno
  En esta tarea, creará la carpeta de trabajo (C:\DeploymentTutorial) y las nuevas variables de entorno del sistema (`DataTransfer` y `LoadXMLData`) que usará en posteriores tareas del tutorial.  
  
 La carpeta de trabajo está en la raíz de la unidad C. Si debe usar otra unidad o ubicación, puede hacerlo. No obstante, deberá anotar esta ubicación y usarla siempre que el tutorial haga referencia a la ubicación de la carpeta de trabajo DeploymentTutorial.  
  
 En una lección posterior implementará paquetes que están guardados en el sistema de archivos en la tabla sysssispackages de la base de datos msdb de[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Lo ideal es que implemente los paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en otro equipo. Si no es posible, puede aprender a hacerlo en este tutorial si implementa los paquetes en una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que se encuentre en el equipo local. Las variables de entorno que se utilizan en el equipo local y de destino tienen los mismos nombres de variable, pero diferentes valores almacenados. Por ejemplo, en el equipo local, el valor de la variable de entorno `DataTransfer` hace referencia a la carpeta C:\DeploymentTutorial, mientras que en el equipo de destino la variable de entorno `DataTransfer` hace referencia a la carpeta C:\DeploymentTutorialInstall.  
  
 Si planea realizar una implementación en el equipo local, solamente necesita crear un conjunto de variables de entorno; no obstante, deberá actualizar el valor de las variables de entorno en un valor apropiado antes de realizar la implementación local.  
  
 Si planea implementar los paquetes en otro equipo, debe crear dos conjuntos de variables de entorno: un conjunto para el equipo local y otro para el equipo de destino. Ahora solamente puede crear las variables para el equipo de origen y, más tarde, crear las variables para el equipo de destino, pero debe tener la carpeta y las variables de entorno disponibles en el equipo de destino antes de poder instalar los paquetes en ese equipo.  
  
### <a name="to-create-the-local-working-folder"></a>Para crear la carpeta de trabajo local  
  
1.  Haga clic con el botón secundario en el menú Inicio y haga clic en Explorar.  
  
2.  Haga clic en **Disco local (C:)**.  
  
3.  En el menú **Archivo** , seleccione **Nuevo**y haga clic en **Carpeta**.  
  
4.  Cambiar el nombre de la nueva carpeta para `DeploymentTutorial`.  
  
### <a name="to-create-local-environment-variables"></a>Para crear variables del entorno local  
  
1.  En el menú **Inicio** , haga clic en **Panel de control**.  
  
2.  En el Panel de control, haga doble clic en **Sistema**.  
  
3.  En el cuadro de diálogo **Propiedades del sistema** , haga clic en la pestaña **Opciones avanzadas** y, a continuación, haga clic en **Variables de entorno**.  
  
4.  En el cuadro de diálogo **Variables de entorno** , en el marco **Variables del sistema** , haga clic en **Nueva**.  
  
5.  En el **nueva Variable del sistema** cuadro de diálogo, escriba `DataTransfer` en el **nombre de Variable** cuadro, y `C:\DeploymentTutorial\datatransferconfig.dtsconfig` en el **valordelavariable** cuadro.  
  
6.  Haga clic en **Aceptar**.  
  
7.  Haga clic en **New** nuevo y el tipo `LoadXMLData` en el **nombre de Variable** cuadro, y `C:\DeploymentTutorial\loadxmldataconfig.dtsconfig` en el **valor de la Variable** cuadro.  
  
8.  Haga clic en **Aceptar** para salir del cuadro de diálogo **Variables de entorno** .  
  
9. Haga clic en **Aceptar** para salir del cuadro de diálogo **Propiedades del sistema** .\  
  
10. Opcionalmente, reinicie el equipo. Si no reinicia el equipo, el nombre de la nueva variable no se mostrará en el Asistente para la configuración de paquetes, pero podrá usarla.  
  
### <a name="to-create-destination-environment-variables"></a>Para crear variables del entorno de destino  
  
1.  En el menú **Inicio** , haga clic en **Panel de control**.  
  
2.  En el Panel de control, haga doble clic en **Sistema**.  
  
3.  En el cuadro de diálogo **Propiedades del sistema** , haga clic en la pestaña **Opciones avanzadas** y, a continuación, haga clic en **Variables de entorno**.  
  
4.  En el cuadro de diálogo **Variables de entorno** , en el marco **Variables del sistema** , haga clic en **Nueva**.  
  
5.  En el **nueva variable del sistema** cuadro de diálogo, escriba `DataTransfer` en el **nombre de Variable** cuadro, y `C:\DeploymentTutorialInstall\datatransferconfig.dtsconfig` en el **valor de la Variable** cuadro.  
  
6.  Haga clic en **Aceptar**.  
  
7.  Haga clic en **New** nuevo y el tipo `LoadXMLData` en el **nombre de Variable** cuadro, y `C:\DeploymentTutorialInstall\loadxmldataconfig.dtsconfig` en el **valor de la Variable** cuadro.  
  
8.  Haga clic en **Aceptar** para salir del cuadro de diálogo **Variables de entorno** .  
  
9. Haga clic en **Aceptar** para salir del cuadro de diálogo **Propiedades del sistema** .\  
  
10. Opcionalmente, reinicie el equipo.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Paso 2: Crear el proyecto de implementación](../integration-services/lesson-1-2-creating-the-deployment-project.md)  
  
![Icono de Integration Services (pequeño)](media/dts-16.gif "icono de Integration Services (pequeño)")**mantenerse actualizado con Integration Services**<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
  
