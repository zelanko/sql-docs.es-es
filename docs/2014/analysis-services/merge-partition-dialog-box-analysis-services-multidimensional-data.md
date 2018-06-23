---
title: Cuadro de diálogo de partición (Analysis Services - datos multidimensionales) de mezcla | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.sqlserverstudio.mergepartition.f1
ms.assetid: 1c94e250-ee18-4f98-b112-985f6346102a
caps.latest.revision: 9
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: aae229b83f367613cc786a3910b00b45e64f31bd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36197720"
---
# <a name="merge-partition-dialog-box-analysis-services---multidimensional-data"></a>Cuadro de diálogo Partición de mezcla (Analysis Services - Datos multidimensionales)
  Utilice el cuadro de diálogo **Partición de mezcla** de **SQL Server Management Studio** para mezclar las particiones de un grupo de medida en un cubo. Para mostrar el cuadro de diálogo **Partición de mezcla** , haga clic con el botón derecho en la carpeta Particiones o en una partición del **Explorador de objetos** y seleccione **Partición de mezcla** en el menú contextual.  
  
## <a name="options"></a>Opciones  
 **Server**  
 Seleccione el nombre de la instancia de Analysis Services que contiene la partición de destino.  
  
 **Nombre**  
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
|**Procesó por última vez**|Muestra la fecha y la hora en que la partición de origen se procesó por última vez.|  
  
## <a name="see-also"></a>Vea también  
 [Las particiones &#40;Analysis Services - datos multidimensionales&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [Mezclar particiones en Analysis Services &#40;SSAS - multidimensionales&#41;](multidimensional-models/merge-partitions-in-analysis-services-ssas-multidimensional.md)  
  
  