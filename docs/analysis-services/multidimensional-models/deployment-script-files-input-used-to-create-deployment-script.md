---
title: Comprender los archivos de entrada utilizados para crear el Script de implementación | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6b75ec5d7433931a81a0fa6e2c648f85335fbedc
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38002197"
---
# <a name="deployment-script-files---input-used-to-create-deployment-script"></a>Archivos de Script de implementación: entrada utilizados para crear Script de implementación
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Cuando se crea un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proyecto, [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] genera archivos para el proyecto. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] coloca estos archivos en la carpeta de salida de la [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proyecto. De manera predeterminada la carpeta de salida está fuera en la carpeta \Bin. En la siguiente tabla se describen los archivos XML que crea [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] .  
  
|Archivo|Descripción|  
|---------------|-----------------|  
|\<*nombre del proyecto*> .asdatabase|Un archivo XMLA para proyectos de modelos tabulares 1100 o 1103 o Multidimensional, o un archivo JSON para Tabular 1200 y superior proyectos de modelos. Contiene las definiciones declarativas para todos los objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se encuentran en el proyecto.|  
|\<*nombre del proyecto*> .deploymenttargets|Contiene el nombre de la base de datos y la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en la que se crearán los objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|\<*nombre del proyecto*> .configsettings|Contiene configuración específica del entorno, como información sobre la conexión del origen de datos y ubicaciones de almacenamiento de objetos. En este archivo de valores de reemplazan el \< *nombre del proyecto*>. asdatabase.|  
|\<*nombre del proyecto*> .deploymentoptions|Contiene opciones de implementación como, por ejemplo, si la implementación es transaccional y si los objetos implementados deben procesarse después de la implementación.|  
  
> [!NOTE]  
>  [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] nunca almacena las contraseñas en sus archivos de proyecto.  
  
## <a name="modifying-the-input-files"></a>Modificar los archivos de entrada  
 Modificar los valores de los archivos de entrada o los valores recuperados de los archivos de entrada, permite cambiar el destino de implementación, los valores de configuración y opciones de implementación sin necesidad de editar todo el \< *proyecto nombre*> archivo .asdatabase (o un archivo de script completo si genera un script de una existente [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos). La posibilidad de modificar archivos individuales le permite crear fácilmente diferentes scripts de implementación para distintos fines.  
  
 En los siguientes temas se explica cómo modificar los valores de los diversos archivos de entrada:  
  
-   [Especificar el destino de instalación](../../analysis-services/multidimensional-models/deployment-script-files-specifying-the-installation-target.md)  
  
-   [Especificar opciones de implementación de roles y particiones](../../analysis-services/multidimensional-models/deployment-script-files-partition-and-role-deployment-options.md)  
  
-   [Especificar la configuración para la implementación de soluciones](../../analysis-services/multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)  
  
-   [Especificar opciones de procesamiento](../../analysis-services/multidimensional-models/deployment-script-files-specifying-processing-options.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejecutar el Asistente para la implementación de Analysis Services](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)   
 [Descripción del script de implementación de Analysis Services](../../analysis-services/multidimensional-models/understanding-the-analysis-services-deployment-script.md)  
  
  
