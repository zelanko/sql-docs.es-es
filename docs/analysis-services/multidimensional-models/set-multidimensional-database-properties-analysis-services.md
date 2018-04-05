---
title: Establecer propiedades de base de datos Multidimensional (Analysis Services) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- properties [Analysis Services], databases
ms.assetid: a8be5b3f-3148-448a-976c-7222705155d9
caps.latest.revision: 24
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 6585737ac1f796b7e9e6e8834d6ca5b5c1c11612
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="set-multidimensional-database-properties-analysis-services"></a>Establecer propiedades de bases de datos multidimensionales (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Hay una serie de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] propiedades que puede configurar en la base de datos la [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] Diseñador de la base de datos.  
  
 En este diseñador puede realizar los tipos de tareas siguientes:  
  
-   Si está conectado a la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en el modo en línea, puede cambiar el nombre de la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Si trabaja en el modo de proyecto, puede cambiar el nombre de la base de datos para la siguiente implementación del proyecto. Para obtener más información, vea [Cambie el nombre de una base de datos multidimensional &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/rename-a-multidimensional-database-analysis-services.md) y [Configurar las propiedades de un proyecto de Analysis Services &#40;SSDT&#41;](../../analysis-services/multidimensional-models/configure-analysis-services-project-properties-ssdt.md).  
  
-   Puede proporcionar una descripción de la base de datos para que la lean los usuarios. También puede ver el nombre de la base de datos, pero no lo puede cambiar. Para cambiar el nombre de la base de datos, debe editar las propiedades del proyecto.  
  
-   Puede proporcionar traducciones para el nombre y la descripción de la base de datos en uno o varios idiomas. Para obtener más información, vea [Traducciones de cubos](../../analysis-services/multidimensional-models-olap-logical-cube-objects/cube-translations.md), [Traducciones de dimensiones](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimension-translations.md)y [Compatibilidad con traducción en Analysis Services](../../analysis-services/translation-support-in-analysis-services.md).  
  
-   Puede ver y modificar las asignaciones de tipo de cuenta predeterminadas. Las asignaciones de tipo de cuenta se usan cuando una o varias medidas usan la función de agregación *ByAccount* . Para cada tipo de cuenta, puede especificar un alias y modificar la función de agregación predeterminada asociada al tipo de cuenta. Para obtener más información sobre cómo modificar la agregación predeterminada, vea [Definir el comportamiento de suma parcial](../../analysis-services/multidimensional-models/define-semiadditive-behavior.md).  
  
## <a name="database-properties"></a>Propiedades de la base de datos  
 Además de las anteriores, hay ciertas propiedades de base de datos que se pueden configurar en la ventana Propiedades.  
  
|Propiedad|Description|  
|--------------|-----------------|  
|Prefijo de agregación|Es el prefijo común que se puede usar en los nombres de agregación de todas las particiones de una base de datos. Para obtener más información, vea [Elemento AggregationPrefix &#40;ASSL&#41;](../../analysis-services/scripting/properties/aggregationprefix-element-assl.md).|  
|Intercalación|Si el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se implementa en una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , la base de datos heredará de la propiedad del servidor Collation, a menos que aquí se proporcione otro valor.|  
|DataSourceImpersonationInfo|Especifica el modo de suplantación predeterminado de todos los objetos de origen de datos de la base de datos. Es el modo que el servicio [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usa al procesar objetos, sincronizar servidores y ejecutar las instrucciones de minería de datos OpenQuery y SystemOpenSchema.|  
|Tamaño estimado|Proporciona un tamaño estimado de los archivos de base de datos en el disco. Si los datos se almacenan en varias ubicaciones, esta estimación se limitará a los archivos de datos almacenados en la carpeta de la base de datos.<br /><br /> **EstimatedSize** se puede utilizar como base para calcular la memoria. Generalmente, los requisitos de memoria son mayores que el tamaño de los datos en el disco debido a las estructuras de datos adicionales que se crean cuando la base de datos se carga en memoria.<br /><br /> Para calcular con más precisión los requisitos de memoria, puede utilizar el Administrador de tareas para examinar la memoria de proceso de Analysis Services antes y después de procesar la base de datos y observar la memoria usada como un método para conocer los requisitos de memoria de la base de datos.|  
|Idioma|Si el proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se implementa en una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , la base de datos heredará de la propiedad del servidor Language, a menos que aquí se proporcione otro valor.|  
|MasterDataSource ID|Se usa con las particiones remotas. Para más información, consulte [Remote Partitions](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md).|  
  
## <a name="see-also"></a>Vea también  
 [Propiedades de la base de datos (cuadro de diálogo) &#40;SSAS: multidimensional&#41;](http://msdn.microsoft.com/library/70f000b7-917f-4699-b142-7a0d13ff767c)   
 [Configurar las propiedades de un proyecto de Analysis Services &#40;SSDT&#41;](../../analysis-services/multidimensional-models/configure-analysis-services-project-properties-ssdt.md)  
  
  
