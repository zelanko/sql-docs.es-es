---
title: "Especificar el destino de instalaci&#243;n | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "archivos de entrada [Analysis Services]"
  - "destinos de instalación [Analysis Services]"
  - "implementaciones de Analysis Services, destinos de instalación"
  - "Asistente para la implementación de Analysis Services, destinos de instalación"
  - "implementar [Analysis Services], destinos de instalación"
  - "destinos de instalación, modificar"
ms.assetid: cb706817-6f63-4771-92c3-b70030bbce3d
caps.latest.revision: 35
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Especificar el destino de instalaci&#243;n
  El Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] lee en el archivo \<*nombre de proyecto*>.deploymenttargets la información del destino de la instalación. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] crea este archivo cuando se genera el proyecto de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] usa la base de datos y el servidor especificados en la página **Implementación** del cuadro de diálogo **Páginas de propiedades** de *\<nombre de proyecto>* para crear el archivo \<*nombre de proyecto*>.targets.  
  
## Modificar el destino de instalación para la implementación  
 En algunas situaciones, puede que necesite implementar un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en una base de datos o en una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que sea diferente a la especificada en la página **Implementación** . Por ejemplo, puede que desee implementar el proyecto en un servidor para realizar pruebas antes de la implementación y, a continuación, implementarlo en un servidor de producción. Puede que también desee implementar un proyecto finalizado y probado en varios servidores de producción de un clúster de equilibrio de carga de red (NLB), o en un servidor de ensayo y un servidor de producción.  
  
 Para implementar un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en una base de datos o una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] diferentes, puede cambiar el destino de instalación del archivo de entrada mediante uno de los métodos descritos en el siguiente procedimiento.  
  
#### Para cambiar el destino de instalación después de haber generado los archivos de entrada  
  
-   Ejecute el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de forma interactiva. En la página **Destino de instalación** , especifique un nuevo destino para la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y la base de datos.  
  
     O bien  
  
-   Ejecute el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en el símbolo del sistema y ajuste el asistente de manera que se ejecute en modo de archivo de respuesta. Para obtener más información acerca del modo de archivo de respuesta, vea [Running the Analysis Services Deployment Wizard](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md).  
  
     O bien  
  
-   Modifique el archivo \<*nombre de proyecto*>.deploymenttargets usando cualquier editor de texto.  
  
## Vea también  
 [Especificar opciones de implementación de roles y particiones](../../analysis-services/multidimensional-models/specifying-partition-and-role-deployment-options.md)   
 [Especificar la configuración para la implementación de soluciones](../../analysis-services/multidimensional-models/specifying-configuration-settings-for-solution-deployment.md)   
 [Especificar opciones de procesamiento](../../analysis-services/multidimensional-models/specifying-processing-options.md)  
  
  