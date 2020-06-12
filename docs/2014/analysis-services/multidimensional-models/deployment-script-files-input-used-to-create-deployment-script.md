---
title: Descripción de los archivos de entrada utilizados para crear el script de implementación | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- input files [Analysis Services]
- Analysis Services Deployment Wizard, scripts
- deploying [Analysis Services], input files
- Analysis Services Deployment Wizard, input files
- scripts [Analysis Services], deployment
- Analysis Services deployments, input files
- modifying input files
ms.assetid: 20e080cd-6a0e-4591-b022-ea4cd3638e36
author: minewiskan
ms.author: owend
ms.openlocfilehash: 2eb377b29ef798b4cbdd02666b866c52eb8f8599
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546883"
---
# <a name="understanding-the-input-files-used-to-create-the-deployment-script"></a>Comprender los archivos de entrada utilizados para crear el script de implementación
  Al compilar un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proyecto [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] de, genera archivos XML para el proyecto. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] coloca estos archivos XML en la carpeta de salida del proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. De manera predeterminada la carpeta de salida está fuera en la carpeta \Bin. En la siguiente tabla se describen los archivos XML que crea [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] .  
  
|Archivo XMLA|Descripción|  
|---------------|-----------------|  
|\<*project name*>. asdatabase|Contiene las definiciones declarativas para todos los objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se encuentran en el proyecto.|  
|\<*project name*>. deploymenttargets|Contiene el nombre de la base de datos y la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en la que se crearán los objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|\<*project name*>. configsettings|Contiene configuración específica del entorno, como información sobre la conexión del origen de datos y ubicaciones de almacenamiento de objetos. La configuración de este archivo invalida la configuración del \<*project name*> archivo. asdatabase.|  
|\<*project name*>. archivo deploymentoptions|Contiene opciones de implementación como, por ejemplo, si la implementación es transaccional y si los objetos implementados deben procesarse después de la implementación.|  
  
> [!NOTE]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] nunca almacena las contraseñas en sus archivos de proyecto.  
  
## <a name="modifying-the-input-files"></a>Modificar los archivos de entrada  
 La modificación de los valores de los archivos de entrada, o de los valores recuperados de los archivos de entrada, permite cambiar el destino de la implementación, los valores de configuración y las opciones de implementación sin editar el \<*project name*> archivo. asdatabase completo (o un archivo de script XMLA completo si se genera un script a partir de una [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos existente). La posibilidad de modificar archivos individuales le permite crear fácilmente diferentes scripts de implementación para distintos fines.  
  
 En los siguientes temas se explica cómo modificar los valores de los diversos archivos de entrada:  
  
-   [Especificar el destino de instalación](deployment-script-files-specifying-the-installation-target.md)  
  
-   [Especificar opciones de implementación de roles y particiones](deployment-script-files-partition-and-role-deployment-options.md)  
  
-   [Especificar la configuración para la implementación de soluciones](deployment-script-files-solution-deployment-config-settings.md)  
  
-   [Especificar opciones de procesamiento](deployment-script-files-specifying-processing-options.md)  
  
## <a name="see-also"></a>Consulte también  
 [Ejecutar el Asistente para la implementación de Analysis Services](running-the-analysis-services-deployment-wizard.md)   
 [Descripción del script de implementación de Analysis Services](understanding-the-analysis-services-deployment-script.md)  
  
  
