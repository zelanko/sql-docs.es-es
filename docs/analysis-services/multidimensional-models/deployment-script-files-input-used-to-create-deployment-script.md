---
title: "Descripción de los archivos de entrada utilizados para crear el Script de implementación | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- input files [Analysis Services]
- Analysis Services Deployment Wizard, scripts
- deploying [Analysis Services], input files
- Analysis Services Deployment Wizard, input files
- scripts [Analysis Services], deployment
- Analysis Services deployments, input files
- modifying input files
ms.assetid: 20e080cd-6a0e-4591-b022-ea4cd3638e36
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: d707429364cdae2bedea584320bb2256c1a9cf99
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="deployment-script-files---input-used-to-create-deployment-script"></a>Archivos de Script de implementación: la entrada que se utiliza para crear el Script de implementación
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Cuando se crea un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proyecto, [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] genera archivos para el proyecto. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]coloca estos archivos en la carpeta de salida de la [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proyecto. De manera predeterminada la carpeta de salida está fuera en la carpeta \Bin. En la siguiente tabla se describen los archivos XML que crea [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] .  
  
|Archivo|Description|  
|---------------|-----------------|  
|\<*nombre del proyecto*> .asdatabase|Un archivo XMLA para proyectos de modelo Tabular 1100 o 1103 o Multidimensional, o un archivo JSON para Tabular 1200 y superior proyectos de modelos. Contiene las definiciones declarativas para todos los objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se encuentran en el proyecto.|  
|\<*nombre del proyecto*> .deploymenttargets|Contiene el nombre de la base de datos y la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en la que se crearán los objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|\<*nombre del proyecto*> .configsettings|Contiene configuración específica del entorno, como información sobre la conexión del origen de datos y ubicaciones de almacenamiento de objetos. En este archivo de valores de reemplazan la \< *nombre del proyecto*>. asdatabase.|  
|\<*nombre del proyecto*> .deploymentoptions|Contiene opciones de implementación como, por ejemplo, si la implementación es transaccional y si los objetos implementados deben procesarse después de la implementación.|  
  
> [!NOTE]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] nunca almacena las contraseñas en sus archivos de proyecto.  
  
## <a name="modifying-the-input-files"></a>Modificar los archivos de entrada  
 Modificar los valores de los archivos de entrada o los valores recuperados de los archivos de entrada, permite cambiar el destino de implementación, las opciones de configuración y opciones de implementación sin necesidad de editar todo el \< *proyecto nombre*> archivo .asdatabase (o un archivo de script completo si genera una secuencia de comandos de otra [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos). La posibilidad de modificar archivos individuales le permite crear fácilmente diferentes scripts de implementación para distintos fines.  
  
 En los siguientes temas se explica cómo modificar los valores de los diversos archivos de entrada:  
  
-   [Especificar el destino de instalación](../../analysis-services/multidimensional-models/deployment-script-files-specifying-the-installation-target.md)  
  
-   [Especificar opciones de implementación de roles y particiones](../../analysis-services/multidimensional-models/deployment-script-files-partition-and-role-deployment-options.md)  
  
-   [Especificar la configuración para la implementación de soluciones](../../analysis-services/multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)  
  
-   [Especificar opciones de procesamiento](../../analysis-services/multidimensional-models/deployment-script-files-specifying-processing-options.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejecutar el Asistente para la implementación de Analysis Services](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)   
 [Descripción del script de implementación de Analysis Services](../../analysis-services/multidimensional-models/understanding-the-analysis-services-deployment-script.md)  
  
  
