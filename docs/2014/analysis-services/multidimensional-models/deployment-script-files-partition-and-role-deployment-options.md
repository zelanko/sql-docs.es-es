---
title: Especificar opciones de implementación de roles y particiones | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- input files [Analysis Services]
- partitions [Analysis Services], deployment options
- Analysis Services deployments, roles
- Analysis Services deployments, partitions
- Analysis Services Deployment Wizard, roles
- Analysis Services Deployment Wizard, partitions
- deploying [Analysis Services], roles
- roles [Analysis Services], deployment options
- deploying [Analysis Services], partitions
- modifying role deployments
- modifying partition deployments
ms.assetid: e9b9ca57-a5cc-4fc0-87b5-305257038d56
author: minewiskan
ms.author: owend
ms.openlocfilehash: f4f2f5bb2f3f39636541d5aea5b931b1dcc72534
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546867"
---
# <a name="specifying-partition-and-role-deployment-options"></a>Especificar opciones de implementación de roles y particiones
  El [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Asistente para la implementación de Lee las opciones de implementación de roles y particiones del \<*project name*> archivo. archivo deploymentoptions. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]crea este archivo al compilar el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proyecto. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]usa las opciones de implementación de particiones y roles del proyecto actual cuando \<*project name*> se crea el archivo. archivo deploymentoptions. Para obtener más información acerca de los valores de configuración, vea [Understanding the Input Files Used to Create the Deployment Script](deployment-script-files-input-used-to-create-deployment-script.md).  
  
## <a name="reviewing-the-partition-and-role-deployment-options"></a>Revisar las opciones de implementación de roles y particiones  
 Entre las opciones de implementación del \<*project name*> archivo. archivo deploymentoptions se incluyen las siguientes:  
  
 **Opciones de implementación de particiones**  
 El \<*project name*> archivo. archivo deploymentoptions especifica si las particiones existentes en la base de datos de destino se conservan o se sobrescriben (valor predeterminado). Si las particiones existentes se conservan, solo se implementarán nuevas particiones, y el diseño de las particiones y agregaciones de todos los grupos de medida existentes permanecerán inalterados.  
  
> [!NOTE]  
>  Si se elimina el grupo de medida en el que existe la partición, la partición se elimina también automáticamente.  
  
 **Opciones de implementación de roles**  
 El \<*project name*> archivo. archivo deploymentoptions especifica una de las siguientes opciones de implementación de roles:  
  
-   Los roles y miembros de roles existentes en la base de datos de destino se conservan, y solo se implementan los roles y miembros de roles nuevos.  
  
-   Todos los miembros y roles existentes en la base de datos de destino se reemplazan por los roles y los miembros implementados.  
  
-   Los roles y miembros de roles existentes en la base de datos de destino se conservan, y no se implementan los roles nuevos.  
  
-   **Nota** Cuando se conservan los roles y los miembros existentes, los permisos asociados con esos roles se restablecen en ninguno. Los permisos de seguridad están incluidos en los objetos que protegen, no en los roles de seguridad a los que están asociados. Para obtener más información acerca de cómo trabajar con este comportamiento mediante el Asistente para la implementación de Analysis Services, vea el apartado sobre la conservación de roles y miembros de Microsoft Knowledge base.  
  
## <a name="modifying-the-partition-and-role-deployment-options"></a>Modificar las opciones de implementación de roles y particiones  
 Es posible que tenga que implementar el [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proyecto con distintas opciones de particiones y roles que las almacenadas en el \<*project name*> archivo. archivo deploymentoptions. Por ejemplo, puede que desee conservar las particiones, los roles y los miembros de roles existentes, en lugar de reemplazar todas las particiones, los roles y los miembros existentes, como se indica en el \<*project name*> archivo. archivo deploymentoptions.  
  
 Para modificar la implementación de particiones y roles en un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proyecto de, no puede cambiar la configuración de particiones y roles del proyecto porque el *\<project name>* cuadro de diálogo **páginas de propiedades** de no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] muestra estas opciones. Si desea cambiar las opciones de implementación de roles y particiones, debe cambiar esta información dentro del \<*project name*> propio archivo. archivo deploymentoptions. En el siguiente procedimiento se describe cómo cambiar las opciones de implementación de roles y particiones en el \<*project name*> archivo. archivo deploymentoptions.  
  
#### <a name="to-change-the-deployment-of-partitions-or-roles-after-the-input-files-have-been-generated"></a>Para cambiar la implementación de particiones o roles después de haber generado los archivos de entrada  
  
-   Ejecute el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de forma interactiva, y en la página **Opciones de implementación de particiones y roles** , especifique nuevas opciones de implementación para las particiones y los roles.  
  
     o bien  
  
-   Ejecute el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en el símbolo del sistema y ajuste el asistente de manera que se ejecute en modo de archivo de respuesta. (Para obtener más información acerca del modo de archivo de respuesta, vea [ejecutar el Asistente para la implementación de Analysis Services](running-the-analysis-services-deployment-wizard.md)).  
  
     o bien  
  
-   Abra el \<*project name*> . archivo deploymentoptions en cualquier editor de texto y cambie manualmente las opciones.  
  
## <a name="see-also"></a>Consulte también  
 [Especificar el destino de instalación](deployment-script-files-specifying-the-installation-target.md)   
 [Especificar los valores de configuración para la implementación de la solución](deployment-script-files-solution-deployment-config-settings.md)   
 [Especificar opciones de procesamiento](deployment-script-files-specifying-processing-options.md)  
  
  
