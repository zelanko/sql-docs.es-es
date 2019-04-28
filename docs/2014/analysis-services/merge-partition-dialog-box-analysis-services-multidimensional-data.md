---
title: Cuadro de diálogo de partición (Analysis Services - datos multidimensionales) de mezcla | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.mergepartition.f1
ms.assetid: 1c94e250-ee18-4f98-b112-985f6346102a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c18ffdaa50c6ee48896f2d2e6e65db46c8fe3349
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62727911"
---
# <a name="merge-partition-dialog-box-analysis-services---multidimensional-data"></a>Cuadro de diálogo Partición de mezcla (Analysis Services - Datos multidimensionales)
  Utilice el cuadro de diálogo **Partición de mezcla** de **SQL Server Management Studio** para mezclar las particiones de un grupo de medida en un cubo. Para mostrar el cuadro de diálogo **Partición de mezcla** , haga clic con el botón derecho en la carpeta Particiones o en una partición del **Explorador de objetos** y seleccione **Partición de mezcla** en el menú contextual.  
  
## <a name="options"></a>Opciones  
 **Server**  
 Seleccione el nombre de la instancia de Analysis Services que contiene la partición de destino.  
  
 **Name**  
 Seleccione el nombre de la partición existente que se utilizará como partición de destino.  
  
 **Carpeta**  
 Muestra el nombre de la carpeta que contiene la partición de destino, si la partición seleccionada en Nombre no utiliza la carpeta predeterminada para la instancia de Analysis Services.  
  
 **Particiones de origen**  
 Muestra una cuadrícula que contiene las particiones de origen que se pueden mezclar con la partición de destino.  
  
> [!NOTE]  
>  Solo se pueden mezclar las particiones que conforman el mismo grupo de medida y que comparten el mismo diseño de agregaciones.  
  
 La cuadrícula contiene las columnas siguientes:  
  
|columna|Descripción|  
|------------|-----------------|  
|**Mezcla**|Seleccione esta columna para mezclar la partición de origen con la de destino.|  
|**Nombre de partición**|Muestra el nombre de la partición de origen.|  
|**Procesado por última vez**|Muestra la fecha y la hora en que la partición de origen se procesó por última vez.|  
  
## <a name="see-also"></a>Vea también  
 [Particiones &#40;Analysis Services - Datos multidimensionales&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [Mezclar particiones en Analysis Services &#40;SSAS - Multidimensional&#41;](multidimensional-models/merge-partitions-in-analysis-services-ssas-multidimensional.md)  
  
  
