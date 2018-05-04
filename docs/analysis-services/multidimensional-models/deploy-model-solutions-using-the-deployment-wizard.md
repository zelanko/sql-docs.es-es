---
title: Implementar soluciones con el Asistente para implementación | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ad96fe095cb264cd5f3d4b05fbd6ab95501bd0ce
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="deploy-model-solutions-using-the-deployment-wizard"></a>Implementar soluciones con el Asistente para la implementación
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  El [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Asistente para la implementación utiliza archivos de salida JSON generados a partir de un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] proyecto como archivos de entrada. Estos archivos de entrada se pueden modificar fácilmente para personalizar la implementación de un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . El script de implementación generado puede ejecutarse inmediatamente o guardarse para su implementación posterior.  

> [!NOTE]
> El [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Asistente/utilidad de implementación se instala con [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) (SSMS). Asegúrese de que está utilizando la versión más reciente. Si se ejecuta desde el símbolo del sistema, de forma predeterminada, la versión más reciente del Asistente para la implementación se instala en C:\Program Files (x86) \Microsoft SQL Server\140\Tools\Binn\ManagementStudio. 
  
 Puede realizar la implementación con el asistente según lo explicado aquí. También puede automatizarla o utilizar la capacidad Sincronizar. Si la base de datos implementada es grande, considere la posibilidad de utilizar particiones en los sistemas de destino. Puede automatizar la creación de la partición y el rellenado mediante el modelo de objeto Tabular (TOM), lenguaje de secuencias de comandos de modelo Tabular (TMSL) y Analysis Management Objects (AMO).  
  
> [!IMPORTANT]  
>  Los archivos de salida ni el script de implementación contiene el Id. de usuario o la contraseña si se especifican en la cadena de conexión para un origen de datos o por motivos de suplantación. Puesto que en este escenario se requieren para el procesamiento, deberá agregar manualmente esta información. Si la implementación no incluye el procesamiento, puede agregar esta información de conexión y suplantación cuando lo desee después de la implementación. Si la implementación incluye el procesamiento, puede agregar esta información en el asistente o en el script de implementación una vez guardado.  
  
## <a name="in-this-section"></a>En esta sección  
 Los siguientes temas describen cómo trabajar con el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , los archivos de entrada y el script de implementación:  
  
|Tema|Description|  
|-----------|-----------------|  
|[Ejecuta al Asistente para la implementación de Analysis Services](../../analysis-services/multidimensional-models/running-the-analysis-services-deployment-wizard.md)|Describe los diversos modos en los que se puede ejecutar el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|[Descripción de los archivos de entrada utilizados para crear el Script de implementación](../../analysis-services/multidimensional-models/deployment-script-files-input-used-to-create-deployment-script.md)|Describe qué archivos utiliza el Asistente para la implementación de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] como valores de entrada, cuáles de esos archivos contiene, y proporciona vínculos con los temas que describen cómo modificar los valores de cada uno de los archivos de entrada.|  
|[Descripción de la secuencia de comandos de implementación de Analysis Services](../../analysis-services/multidimensional-models/understanding-the-analysis-services-deployment-script.md)|Describe lo que contiene el script de implementación y cómo se ejecuta este.|  
  
## <a name="see-also"></a>Vea también  
 [Implementar soluciones de modelo mediante XMLA](../../analysis-services/multidimensional-models/deploy-model-solutions-using-xmla.md)   
 [Sincronizar bases de datos de Analysis Services](../../analysis-services/multidimensional-models/synchronize-analysis-services-databases.md)   
 [Descripción de los archivos de entrada utilizados para crear el Script de implementación](../../analysis-services/multidimensional-models/deployment-script-files-input-used-to-create-deployment-script.md)   
 [Implementar soluciones de modelos con la utilidad de implementación](../../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)  
  
  
