---
title: "Especificar opciones de implementación de roles y particiones | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d6595d80eeba45415ac501182c31025478899711
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="deployment-script-files---partition-and-role-deployment-options"></a>Archivos de Script de implementación - opciones de implementación de roles y particiones
  El [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Asistente para implementación de lee las opciones de implementación de roles y particiones de la \< *nombre del proyecto*>. deploymentoptions. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] crea este archivo cuando se genera el proyecto de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]utiliza las opciones de implementación de particiones y roles del actual proyecto cuando el \< *nombre del proyecto*>. deploymentoptions se crean. Para obtener más información acerca de los valores de configuración, vea [Understanding the Input Files Used to Create the Deployment Script](../../analysis-services/multidimensional-models/deployment-script-files-input-used-to-create-deployment-script.md).  
  
## <a name="reviewing-the-partition-and-role-deployment-options"></a>Revisar las opciones de implementación de roles y particiones  
 Las opciones de implementación del \< *nombre del proyecto*> .deploymentoptions file incluyen lo siguiente:  
  
 **Opciones de implementación de particiones**  
 El \< *nombre del proyecto*> .deploymentoptions especifica si las particiones existentes en la base de datos de destino se conservan o sobrescriben (valor predeterminado). Si las particiones existentes se conservan, solo se implementarán nuevas particiones, y el diseño de las particiones y agregaciones de todos los grupos de medida existentes permanecerán inalterados.  
  
> [!NOTE]  
>  Si se elimina el grupo de medida en el que existe la partición, la partición se elimina también automáticamente.  
  
 **Opciones de implementación de roles**  
 El \< *nombre del proyecto*> .deploymentoptions especifica una de las siguientes opciones de implementación de roles:  
  
-   Los roles y miembros de roles existentes en la base de datos de destino se conservan, y solo se implementan los roles y miembros de roles nuevos.  
  
-   Todos los miembros y roles existentes en la base de datos de destino se reemplazan por los roles y los miembros implementados.  
  
-   Los roles y miembros de roles existentes en la base de datos de destino se conservan, y no se implementan los roles nuevos.  
  
-   **Nota** Cuando se conservan los roles y los miembros existentes, los permisos asociados con esos roles se restablecen en ninguno. Los permisos de seguridad están incluidos en los objetos que protegen, no en los roles de seguridad a los que están asociados. Para obtener más información acerca de cómo trabajar con este comportamiento mediante el Asistente para la implementación de Analysis Service, consulte el artículo sobre la retención de roles y miembros de Microsoft Knowledge Base.  
  
## <a name="modifying-the-partition-and-role-deployment-options"></a>Modificar las opciones de implementación de roles y particiones  
 Puede que tenga que implementar el [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proyecto usando las opciones de partición y roles diferentes a las almacenadas en el \< *nombre del proyecto*>. deploymentoptions. Por ejemplo, puede que desee conservar las particiones existentes, roles y los miembros del rol, en lugar de reemplazar todas las particiones existentes, roles y miembros tal como se indica en la \< *nombre del proyecto*>. deploymentoptions.  
  
 Para modificar la implementación de particiones y roles en un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proyecto, no puede cambiar la configuración de particiones y roles dentro del proyecto porque el  *\<nombre del proyecto >* **páginas de propiedades**  cuadro de diálogo de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] no muestra estas opciones. Si desea cambiar las opciones de implementación de roles y particiones, deberá cambiar esta información dentro de la \< *nombre del proyecto*> el propio archivo. deploymentoptions. El siguiente procedimiento describe cómo cambiar las opciones de implementación de particiones y roles dentro de la \< *nombre del proyecto*>. deploymentoptions.  
  
#### <a name="to-change-the-deployment-of-partitions-or-roles-after-the-input-files-have-been-generated"></a>Para cambiar la implementación de particiones o roles después de haber generado los archivos de entrada  
  
-   Ejecute el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de forma interactiva, y en la página **Opciones de implementación de particiones y roles** , especifique nuevas opciones de implementación para las particiones y los roles.  
  
     O bien  
  
-   Ejecute el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en el símbolo del sistema y ajuste el asistente de manera que se ejecute en modo de archivo de respuesta. (Para más información sobre el modo de archivo de respuesta, vea [Ejecutar el Asistente para la implementación de Analysis Services](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)).  
  
     O bien  
  
-   Abra la \< *nombre del proyecto*> .deploymentoptions en cualquier editor de texto y manualmente cambiar las opciones.  
  
## <a name="see-also"></a>Vea también  
 [Especificar el destino de instalación](../../analysis-services/multidimensional-models/deployment-script-files-specifying-the-installation-target.md)   
 [Especificar la configuración de implementación de soluciones](../../analysis-services/multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)   
 [Especificar opciones de procesamiento](../../analysis-services/multidimensional-models/deployment-script-files-specifying-processing-options.md)  
  
  

