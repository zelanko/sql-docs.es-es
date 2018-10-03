---
title: Crear una utilidad de implementación | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- deploying packages [Integration Services], deployment utility
- deployment utility [Integration Services]
ms.assetid: 354322a4-ae8c-4d92-8e71-42d29dbd0614
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: fe7bd725bc7fc9be7289c4834a3df8f44e36c41b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48102205"
---
# <a name="create-a-deployment-utility"></a>Create a Deployment Utility
  El primer paso para implementar paquetes es crear una utilidad de implementación para un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . La utilidad de implementación es una carpeta que contiene los archivos necesarios para implementar los paquetes de un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en un servidor distinto. La utilidad de implementación se crea en el equipo en el que se almacena el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
 Puede crear una utilidad de implementación de paquetes para un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] configurando primero el proceso de generación de una utilidad de implementación y después, generando el proyecto. Al generar el proyecto, todos los paquetes y configuraciones de paquetes del proyecto se incluyen automáticamente. Para implementar archivos adicionales con el proyecto, como un archivo Léame, coloque los archivos en la carpeta **Miscellaneous** del proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Al generar el proyecto, estos archivos también se incluirán automáticamente.  
  
 Puede configurar de manera distinta la implementación de cada proyecto. Antes de generar el proyecto y de crear la utilidad de implementación de paquetes, puede establecer sus propiedades para personalizar la forma en que se implementarán los paquetes en el proyecto. Por ejemplo, puede especificar si desea que las configuraciones de paquetes se actualicen al implementar el proyecto. Para tener acceso a las propiedades de un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , haga clic con el botón derecho en el proyecto y, después, haga clic en **Propiedades**.  
  
 En la tabla siguiente se muestran las propiedades de la utilidad de implementación.  
  
|Property|Descripción|  
|--------------|-----------------|  
|AllowConfigurationChange|Valor que especifica si se actualizarán las configuraciones durante la implementación.|  
|CreateDeploymentUtility|Valor que especifica si se creará una utilidad de implementación de paquetes al generar el proyecto. Esta propiedad debe estar establecida en `True` para crear una utilidad de implementación.|  
|DeploymentOutputPath|Ubicación, respecto al proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , de la utilidad de implementación.|  
  
 Al generar un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], se crea un archivo de manifiesto, \<nombre del proyecto>.SSISDeploymentManifest.xml, junto con las copias de los paquetes del proyecto y las dependencias del paquete, y se agrega a la carpeta bin\Deployment del proyecto o a la ubicación especificada en la propiedad DeploymentOutputPath. El archivo de manifiesto muestra los paquetes, las configuraciones de paquetes y todos los demás archivos del proyecto.  
  
 El contenido de la carpeta de implementación se actualiza cada vez que genera el proyecto. Esto significa que se eliminará cualquier archivo guardado en esta carpeta que no se copie nuevamente en el proceso de generación. Por ejemplo, se eliminarán archivos de configuración de paquetes guardados en las carpetas de implementación.  
  
### <a name="to-create-a-package-deployment-utility"></a>Para crear una utilidad de implementación de paquetes  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra la solución que contiene el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para el que desee crear una utilidad de implementación de paquetes.  
  
2.  Haga clic con el botón derecho en el proyecto y haga clic en **Propiedades**.  
  
3.  En el cuadro de diálogo **\<nombre del proyecto> Páginas de propiedades**, haga clic en **Utilidad de implementación**.  
  
4.  Para actualizar las configuraciones de paquetes cuando se implementan paquetes, establezca **AllowConfigurationChanges** a `True`.  
  
5.  Establecer `CreateDeploymentUtility` a `True`.  
  
6.  Opcionalmente, actualice la ubicación de la utilidad de implementación modificando la propiedad `DeploymentOutputPath`.  
  
7.  Haga clic en **Aceptar**.  
  
8.  En el Explorador de soluciones, haga clic con el botón derecho en el proyecto y, después, haga clic en **Generar**.  
  
9. Vea el progreso y los errores de la generación en la ventana **Salida** .  
  
## <a name="see-also"></a>Vea también  
 [Configuraciones de paquetes](../../2014/integration-services/package-configurations.md)   
 [Crear configuraciones de paquetes](../../2014/integration-services/create-package-configurations.md)   
 [Implementar los paquetes mediante la utilidad de implementación](../../2014/integration-services/deploy-packages-by-using-the-deployment-utility.md)   
 [Implementación del paquete &#40;SSIS&#41;](packages/legacy-package-deployment-ssis.md)  
  
  
