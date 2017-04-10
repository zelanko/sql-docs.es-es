---
title: "Comprender los archivos de entrada utilizados para crear el script de implementaci&#243;n | Microsoft Docs"
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
  - "Asistente para la implementación de Analysis Services, scripts"
  - "implementar [Analysis Services], archivos de entrada"
  - "Asistente para la implementación de Analysis Services, archivos de entrada"
  - "scripts [Analysis Services], implementación"
  - "implementaciones de Analysis Services, archivos de entrada"
  - "archivos de entrada, modificar"
ms.assetid: 20e080cd-6a0e-4591-b022-ea4cd3638e36
caps.latest.revision: 34
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Comprender los archivos de entrada utilizados para crear el script de implementaci&#243;n
  Cuando se crea un proyecto de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] genera archivos XML para el proyecto. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] coloca estos archivos XML en la carpeta de salida del proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . De manera predeterminada la carpeta de salida está fuera en la carpeta \\Bin. En la siguiente tabla se describen los archivos XML que crea [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] .  
  
|Archivo XMLA|Description|  
|---------------|-----------------|  
|\<*nombre del proyecto*\>.asdatabase|Contiene las definiciones declarativas para todos los objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se encuentran en el proyecto.|  
|\<*nombre del proyecto*\>.deploymenttargets|Contiene el nombre de la base de datos y la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en la que se crearán los objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|\<*nombre del proyecto*\>.configsettings|Contiene configuración específica del entorno, como información sobre la conexión del origen de datos y ubicaciones de almacenamiento de objetos. Los valores de este archivo reemplazan a los del archivo \<*nombre del proyecto*\>.asdatabase.|  
|\<*nombre del proyecto*\>.deploymentoptions|Contiene opciones de implementación como, por ejemplo, si la implementación es transaccional y si los objetos implementados deben procesarse después de la implementación.|  
  
> [!NOTE]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] nunca almacena las contraseñas en sus archivos de proyecto.  
  
## Modificar los archivos de entrada  
 Modificar los valores de los archivos de entrada, o de los valores recuperados de los archivos de entrada, permite cambiar el destino de la implementación, los valores de configuración y las opciones de implementación sin necesidad de editar todo el archivo \<*nombre del proyecto*\>.asdatabase \(o todo un archivo de script XMLA en caso de haber generado un script de una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] existente\). La posibilidad de modificar archivos individuales le permite crear fácilmente diferentes scripts de implementación para distintos fines.  
  
 En los siguientes temas se explica cómo modificar los valores de los diversos archivos de entrada:  
  
-   [Especificar el destino de instalación](../../analysis-services/multidimensional-models/specifying-the-installation-target.md)  
  
-   [Especificar opciones de implementación de roles y particiones](../../analysis-services/multidimensional-models/specifying-partition-and-role-deployment-options.md)  
  
-   [Especificar la configuración para la implementación de soluciones](../../analysis-services/multidimensional-models/specifying-configuration-settings-for-solution-deployment.md)  
  
-   [Especificar opciones de procesamiento](../../analysis-services/multidimensional-models/specifying-processing-options.md)  
  
## Vea también  
 [Ejecutar el Asistente para la implementación de Analysis Services](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)   
 [Descripción del script de implementación de Analysis Services](../../analysis-services/multidimensional-models/understanding-the-analysis-services-deployment-script.md)  
  
  