---
title: Especifique los criterios de consulta (Asistente para optimización basada en uso) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.usagebasedoptimizationwizard.specifyquerycriteria.f1
ms.assetid: 3193adc2-af9f-4234-a4cc-dea0c280a724
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 088d53d1257c4b0d4b141b1e090ab1174416d397
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48088385"
---
# <a name="specify-query-criteria-usage-based-optimization-wizard"></a>Especificar los criterios de consulta (Asistente para optimización basada en el uso)
  Use la página **Especificar los criterios de consulta** para elegir una o más opciones de filtro con objeto de identificar las consultas que se deben optimizar.  
  
> [!NOTE]  
>  Esta página esta deshabilitada si [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no puede conectarse al registro de consultas.  
  
## <a name="options"></a>Opciones  
 **Estadísticas del registro de consultas**  
 Muestra información acerca de las consultas almacenadas en el registro de consultas para las particiones seleccionadas. Aparecen los siguientes elementos:  
  
|Término|Definición|  
|----------|----------------|  
|**Total de consultas**|Muestra el número total de consultas almacenadas en el registro de consultas para las particiones seleccionadas.|  
|**Consultas distintivas**|Muestra el número de consultas distintivas almacenadas en el registro de consultas para las particiones seleccionadas.|  
|**Usuarios distintivos**|Muestra el número total de usuarios distintivos asociados con las consultas almacenadas en el registro de consultas para las particiones seleccionadas.|  
|**Tiempo medio de respuesta**|Muestra el tiempo de respuesta promedio para las consultas distintivas almacenadas en el registro de consultas para las particiones seleccionadas.|  
  
 **Fecha de inicio**  
 Filtra consultas en el registro de consultas basándose en una fecha y hora de inicio. Elija o escriba una fecha en la lista desplegable.  
  
> [!NOTE]  
>  Si no se selecciona la **Fecha de finalización** , se tienen en cuenta todas las consultas del registro de consultas de la fecha y hora especificada en esta opción o posteriores a esta.  
  
 **Fecha de finalización**  
 Filtra consultas en el registro de consultas basándose en una fecha y hora de finalización. Elija o escriba una fecha en la lista desplegable.  
  
> [!NOTE]  
>  Si no se selecciona la **Fecha de inicio** , se tienen en cuenta todas las consultas del registro de consultas de la fecha y hora especificada en esta opción o anteriores a esta.  
  
 **Usuarios**  
 Filtra consultas en el registro de consultas basándose en un conjunto de usuarios especificado. Haga clic en el botón de puntos suspensivos (**...**) para mostrar el cuadro de diálogo **Selección de usuarios** y elegir los usuarios sobre los que filtrar las consultas. Para obtener más información sobre el cuadro de diálogo **Selección de usuarios**, vea [Cuadro de diálogo Selección de usuarios &#40;Analysis Services - Datos multidimensionales&#41;](user-selection-dialog-box-analysis-services-multidimensional-data.md).  
  
 **Consultas más frecuentes**  
 Filtra consultas en el registro de consultas basándose en el porcentaje más alto de consultas distintas que se han ejecutado con más frecuencia en las particiones seleccionadas. Elija o escriba un valor de porcentaje en el cuadro de texto.  
  
## <a name="see-also"></a>Vea también  
 [Ayuda de F1 del Asistente para optimización basada en uso](usage-based-optimization-wizard-f1-help.md)   
 [Asistentes de Analysis Services &#40;datos multidimensionales&#41;](analysis-services-wizards-multidimensional-data.md)  
  
  
