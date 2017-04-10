---
title: "Especificar opciones de implementaci&#243;n de roles y particiones | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "archivos de entrada [Analysis Services]"
  - "particiones [Analysis Services], opciones de implementación"
  - "implementaciones de Analysis Services, roles"
  - "implementaciones de Analysis Services, particiones"
  - "Asistente para la implementación de Analysis Services, roles"
  - "Asistente para la implementación de Analysis Services, particiones"
  - "implementación [Analysis Services], roles"
  - "roles [Analysis Services], opciones de implementación"
  - "implementación [Analysis Services], particiones"
  - "implementaciones de roles, modificar"
  - "implementaciones de particiones, modificar"
ms.assetid: e9b9ca57-a5cc-4fc0-87b5-305257038d56
caps.latest.revision: 37
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Especificar opciones de implementaci&#243;n de roles y particiones
  El Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] lee las opciones de implementación de roles y particiones en el archivo \<*nombre de proyecto*>.deploymentoptions. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] crea este archivo cuando se genera el proyecto de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] usa las opciones de implementación de roles y particiones del proyecto actual cuando se crea el archivo \<*nombre de proyecto*>.deploymentoptions. Para obtener más información acerca de los valores de configuración, vea [Understanding the Input Files Used to Create the Deployment Script](../../analysis-services/multidimensional-models/understanding-the-input-files-used-to-create-the-deployment-script.md).  
  
## Revisar las opciones de implementación de roles y particiones  
 Las opciones de implementación del archivo \<*nombre de proyecto*>.deploymentoptions file incluyen las siguientes:  
  
 **Opciones de implementación de particiones**  
 El archivo \<*nombre de proyecto*>.deploymentoptions especifica si las particiones existentes de la base de datos de destino se conservan o sobrescriben (valor predeterminado). Si las particiones existentes se conservan, solo se implementarán nuevas particiones, y el diseño de las particiones y agregaciones de todos los grupos de medida existentes permanecerán inalterados.  
  
> [!NOTE]  
>  Si se elimina el grupo de medida en el que existe la partición, la partición se elimina también automáticamente.  
  
 **Opciones de implementación de roles**  
 El archivo \<*nombre de proyecto*>.deploymentoptions especifica una de las siguientes opciones de implementación de roles:  
  
-   Los roles y miembros de roles existentes en la base de datos de destino se conservan, y solo se implementan los roles y miembros de roles nuevos.  
  
-   Todos los miembros y roles existentes en la base de datos de destino se reemplazan por los roles y los miembros implementados.  
  
-   Los roles y miembros de roles existentes en la base de datos de destino se conservan, y no se implementan los roles nuevos.  
  
-   **Nota** Cuando se conservan los roles y los miembros existentes, los permisos asociados con esos roles se restablecen en ninguno. Los permisos de seguridad están incluidos en los objetos que protegen, no en los roles de seguridad a los que están asociados. Para obtener más información acerca de cómo trabajar con este comportamiento mediante el Asistente para la implementación de Analysis Service, consulte el artículo sobre la retención de roles y miembros de Microsoft Knowledge Base.  
  
## Modificar las opciones de implementación de roles y particiones  
 Puede que tenga que implementar el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] con opciones de particiones y roles diferentes a las almacenadas en el archivo \<*nombre de proyecto*>.deploymentoptions. Por ejemplo, puede que quiera conservar las particiones, los roles y los miembros de roles existentes, en lugar de reemplazar todos los miembros, roles y particiones existentes según lo indicado en el archivo \<*nombre de proyecto*>.deploymentoptions.  
  
 Para modificar la implementación de particiones y roles en un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], no puede cambiar la configuración de los roles y particiones del proyecto porque el cuadro de diálogo **Páginas de propiedades** de *\<nombre de proyecto>* en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] no muestra estas opciones. Si quiere cambiar las opciones de implementación para roles y particiones, deberá cambiar esta información dentro del propio archivo \<*nombre de proyecto*>.deploymentoptions. El siguiente procedimiento describe cómo cambiar las opciones de implementación de particiones y roles del archivo \<*nombre de proyecto*>.deploymentoptions.  
  
#### Para cambiar la implementación de particiones o roles después de haber generado los archivos de entrada  
  
-   Ejecute el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de forma interactiva, y en la página **Opciones de implementación de particiones y roles** , especifique nuevas opciones de implementación para las particiones y los roles.  
  
     O bien  
  
-   Ejecute el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en el símbolo del sistema y ajuste el asistente de manera que se ejecute en modo de archivo de respuesta. (Para más información sobre el modo de archivo de respuesta, vea [Ejecutar el Asistente para la implementación de Analysis Services](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)).  
  
     O bien  
  
-   Abra el archivo \<*nombre de proyecto*>.deploymentoptions en cualquier editor de texto y cambie las opciones de forma manual.  
  
## Vea también  
 [Especificar el destino de instalación](../../analysis-services/multidimensional-models/specifying-the-installation-target.md)   
 [Especificar la configuración para la implementación de soluciones](../../analysis-services/multidimensional-models/specifying-configuration-settings-for-solution-deployment.md)   
 [Especificar opciones de procesamiento](../../analysis-services/multidimensional-models/specifying-processing-options.md)  
  
  