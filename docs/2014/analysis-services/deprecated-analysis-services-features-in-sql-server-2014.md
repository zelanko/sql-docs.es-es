---
title: Características en desuso de Analysis Services en SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Analysis Services, backward compatibility
- SSAS, backward compatibility
- SQL Server Analysis Services, backward compatibility
- deprecated features [Analysis Services]
ms.assetid: 2c96ecfe-a170-41d0-bee3-74503f880197
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 04d12aab677e38d17d4e869e6885eb470854d824
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66081918"
---
# <a name="deprecated-analysis-services-features-in-sql-server-2014"></a>Características en desuso de Analysis Services en SQL Server 2014
  Este tema describe las características desusadas de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que siguen estando disponibles en [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Está previsto quitar estas características en una futura versión de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Las características en desuso no se deben usar en nuevas aplicaciones.  
  
## <a name="features-not-supported-in-the-next-version-of-sql-server"></a>Características no admitidas en la siguiente versión de SQL Server  
 Las características del [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] siguientes no se admitirán en la siguiente versión de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. No utilice estas características en nuevos trabajos de desarrollo y modifique lo antes posible las aplicaciones que las utilizan actualmente.  
  
|Category|Característica desusada|Sustituta|  
|--------------|------------------------|-----------------|  
|Función MDX|Función CalculationPassValue|Ninguno. El motor de OLAP administra el paso de cálculo. Esta función ya no se necesita.|  
|Función MDX|CalculationCurrentPass, función|Ninguno. El motor de OLAP administra el paso de cálculo. Esta función ya no se necesita.|  
|Expresiones multidimensionales (MDX)|La sugerencia del optimizador de consultas NON_EMPTY_BEHAVIOR estaba activada de forma predeterminada.|La sugerencia del optimizador de consultas NON_EMPTY_BEHAVIOR estará desactivada de forma predeterminada en una futura versión. Se trata de una sugerencia de optimización MDX que puede generar resultados incorrectos si no se usa correctamente.|  
|Otros|Propiedad de celda intrínseca CELL_EVALUATION_LIST|Se proporcionaba originalmente una lista de las fórmulas evaluadas que se aplican a una celda. Está en blanco en esta versión de Analysis Services.  El orden de resolución se especifica en un script MDX. Para obtener más información, consulte [descripción de orden de paso y orden de resolución &#40;MDX&#41;](multidimensional-models/mdx/mdx-data-manipulation-understanding-pass-order-and-solve-order.md)|  
|Objetos|Ensamblados COM|Los ensamblados COM pueden suponer un riesgo para la seguridad. Compatibilidad con los ensamblados COM se quitará en una versión futura.|  
  
## <a name="features-not-supported-in-a-future-version-of-sql-server"></a>Características no admitidas en una versión futura de SQL Server  
 Las características del [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] siguientes se admiten en la próxima versión de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], pero se quitarán en una versión posterior. No se ha determinado la versión específica de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
|Category|Característica desusada|Sustituta|  
|--------------|------------------------|-----------------|  
|Modelos multidimensionales|Particiones remotas|Ninguno. Use particiones locales en su lugar. Consulte [crear y administrar una partición Local &#40;Analysis Services&#41; ](multidimensional-models/create-and-manage-a-local-partition-analysis-services.md) para obtener más información.|  
|Modelos multidimensionales|Grupos de medida vinculados remotos|Un grupo de medida vinculado remoto es un grupo de medida vinculado que usa un origen de datos de un servidor remoto. Está previsto desusar la posibilidad de usar un origen de datos remoto para un grupo de medida vinculado.<br /><br /> No hay ningún reemplazo para esta característica. Se recomienda usar grupos de medida vinculados locales en su lugar. Consulte [Linked Measure Groups](multidimensional-models/linked-measure-groups.md) para obtener más información.|  
|Modelos multidimensionales|Reescritura de dimensiones|Ninguno. Use la reescritura de particiones si necesita la capacidad de reescritura. Consulte [Set Partition Writeback](multidimensional-models/set-partition-writeback.md) para obtener más información.|  
|Modelos multidimensionales|Dimensiones vinculadas|Ninguno. Considere la posibilidad de copiar dimensiones a modelos adicionales en lugar de vincularse a una dimensión de otro modelo.|  
|MDX|Propiedad Non_Empty_Behavior|Ninguno. Al crear un miembro calculado, establecer esta propiedad incorrectamente aumenta la probabilidad de devolver resultados no válidos. Las optimizaciones recientes para el motor OLAP han mejorado las operaciones en conjuntos de datos dispersos, lo que hace que esta propiedad sea menos relevante.|  
  
## <a name="see-also"></a>Vea también  
 [Compatibilidad con versiones anteriores de Analysis Services](analysis-services-backward-compatibility.md)   
 [Funcionalidad no incluida Analysis Services en SQL Server 2014](discontinued-analysis-services-functionality-in-sql-server-2014.md)  
  
  
