---
title: Especificar opciones de implementación de roles y particiones | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
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
manager: craigg
ms.openlocfilehash: 66c2683bd383ebd3d0a9278cb008b6909dc80007
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62726299"
---
# <a name="specifying-partition-and-role-deployment-options"></a>Especificar opciones de implementación de roles y particiones
  El [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Asistente para implementación de lee las opciones de implementación de particiones y roles en el \< *nombre del proyecto*> .deploymentoptions file. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] crea este archivo cuando se genera el proyecto de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] usa las opciones de implementación de roles y particiones del actual proyecto cuando el \< *nombre del proyecto*> .deploymentoptions file se crea. Para obtener más información acerca de los valores de configuración, vea [Comprender los archivos de entrada utilizados para crear el script de implementación](deployment-script-files-input-used-to-create-deployment-script.md).  
  
## <a name="reviewing-the-partition-and-role-deployment-options"></a>Revisar las opciones de implementación de roles y particiones  
 Las opciones de implementación el \< *nombre del proyecto*> .deploymentoptions file incluyen las siguientes:  
  
 **Opciones de implementación de particiones**  
 El \< *nombre del proyecto*> .deploymentoptions especifica si se conservan las particiones existentes de la base de datos de destino o sobrescriben (valor predeterminado). Si las particiones existentes se conservan, solo se implementarán nuevas particiones, y el diseño de las particiones y agregaciones de todos los grupos de medida existentes permanecerán inalterados.  
  
> [!NOTE]  
>  Si se elimina el grupo de medida en el que existe la partición, la partición se elimina también automáticamente.  
  
 **Opciones de implementación de roles**  
 El \< *nombre del proyecto*> .deploymentoptions especifica una de las siguientes opciones de implementación de roles:  
  
-   Los roles y miembros de roles existentes en la base de datos de destino se conservan, y solo se implementan los roles y miembros de roles nuevos.  
  
-   Todos los miembros y roles existentes en la base de datos de destino se reemplazan por los roles y los miembros implementados.  
  
-   Los roles y miembros de roles existentes en la base de datos de destino se conservan, y no se implementan los roles nuevos.  
  
-   **Nota** Cuando se conservan los roles y los miembros existentes, los permisos asociados con esos roles se restablecen en ninguno. Los permisos de seguridad están incluidos en los objetos que protegen, no en los roles de seguridad a los que están asociados. Para obtener más información sobre cómo trabajar con este comportamiento mediante el Asistente para la implementación del servicio de análisis, vea "Retención de Roles y miembros" en Microsoft Knowledge Base.  
  
## <a name="modifying-the-partition-and-role-deployment-options"></a>Modificar las opciones de implementación de roles y particiones  
 Es posible que deba implementar el [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proyecto usando las opciones de particiones y roles diferentes a las almacenadas en el \< *nombre del proyecto*> .deploymentoptions file. Por ejemplo, es posible que desee conservar las particiones existentes, los roles y los miembros del rol, en lugar de reemplazar todos los miembros, roles y particiones existentes según lo indicado en el \< *nombre del proyecto*> .deploymentoptions file.  
  
 Para modificar la implementación de particiones y roles en un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proyecto, no puede cambiar la configuración de particiones y roles dentro del proyecto porque el  *\<nombre del proyecto >* **las páginas de propiedades**  cuadro de diálogo de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] no muestra estas opciones. Si desea cambiar las opciones de implementación para roles y particiones, debe cambiar esta información dentro de la \< *nombre del proyecto*> .deploymentoptions file propio. El siguiente procedimiento describe cómo cambiar las opciones de implementación de particiones y roles dentro de la \< *nombre del proyecto*> .deploymentoptions file.  
  
#### <a name="to-change-the-deployment-of-partitions-or-roles-after-the-input-files-have-been-generated"></a>Para cambiar la implementación de particiones o roles después de haber generado los archivos de entrada  
  
-   Ejecute el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de forma interactiva, y en la página **Opciones de implementación de particiones y roles** , especifique nuevas opciones de implementación para las particiones y los roles.  
  
     -o bien-  
  
-   Ejecute el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en el símbolo del sistema y ajuste el asistente de manera que se ejecute en modo de archivo de respuesta. (Para más información sobre el modo de archivo de respuesta, vea [Ejecutar el Asistente para la implementación de Analysis Services](running-the-analysis-services-deployment-wizard.md)).  
  
     -o bien-  
  
-   Abra el \< *nombre del proyecto*> .deploymentoptions en cualquier editor de texto y manualmente cambiar las opciones.  
  
## <a name="see-also"></a>Vea también  
 [Especificar el destino de instalación](deployment-script-files-specifying-the-installation-target.md)   
 [Especificar la configuración para la implementación de soluciones](deployment-script-files-solution-deployment-config-settings.md)   
 [Especificar opciones de procesamiento](deployment-script-files-specifying-processing-options.md)  
  
  
