---
title: Finalización del asistente (Asistente para particiones) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitionwizard.finish.f1
ms.assetid: 68a4dd5d-94d9-4a02-be31-949a6da0ef51
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f7ab4ad7a819c18056ab5901f95caf1b74b23a25
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66087525"
---
# <a name="completing-the-wizard-partition-wizard"></a>Finalización del asistente (Asistente para particiones)
  Use la página **Finalización del asistente** para asignar un nombre a la partición, definir el diseño de agregaciones para la partición y, opcionalmente, implementar y procesar la partición después de completar el Asistente para particiones.  
  
## <a name="options"></a>Opciones  
 **Nombre**  
 Escriba el nombre para la nueva partición. Si está trabajando con múltiples tablas, escriba el prefijo que se combinará con el nombre de la tabla para crear el nombre de cada partición.  
  
 **Opciones de agregaciones**  
 Especifica la opción de agregación para la partición.  
  
 En la tabla siguiente se enumeran las opciones de agregación disponibles.  
  
|Opción|Descripción|  
|------------|-----------------|  
|**Diseñar las agregaciones de la partición ahora**|Diseña las agregaciones para la nueva partición después de que el Asistente para particiones cree la nueva partición. Al seleccionar esta opción se inicia el Asistente para diseñar agregaciones después de hacer clic en **Finalizar** en el Asistente para particiones. Para más información sobre el Asistente para diseñar agregaciones, vea [Asistente para diseñar agregaciones (Ayuda F1, SSAS)](aggregation-design-wizard-f1-help.md).|  
|**Diseñar las agregaciones posteriormente**|Crea la partición sin diseñar agregaciones en este momento.|  
|**Copiar el diseño de las agregaciones de una partición existente**|Copia en al nueva partición el diseño de agregaciones de una partición existente en el grupo de medida. Al hacer clic en esta opción, se habilita la opción **Copiar de** . Utilice la opción **Copiar de** para seleccionar la partición desde la cual se va a copiar el diseño de agregaciones.<br /><br /> Tenga en cuenta que las particiones que se puedan mezclar en el futuro deben tener la misma estructura de tabla y el mismo diseño de agregaciones. Si desea mezclar la nueva partición con una partición existente en el grupo de medida, deberá copiar el diseño de agregaciones de la partición existente en la partición nueva.|  
  
 **Implementar y procesar ahora**  
 Implementa y procesa la partición en la instancia de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] especificada en la página **Ubicaciones de procesamiento y almacenamiento**. El asistente implementa y procesa la partición una vez que se ha hecho clic en **Finalizar** en esta página.  
  
## <a name="see-also"></a>Consulte también  
 [Particiones &#40;Analysis Services de datos multidimensionales&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)  
  
  
