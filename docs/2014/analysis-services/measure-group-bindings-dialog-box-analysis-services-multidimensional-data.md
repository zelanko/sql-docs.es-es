---
title: Cuadro de diálogo enlaces de grupo de medida (Analysis Services - datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.dimensionusage.definerelationship.measuregroupbindings.f1
helpviewer_keywords:
- Measure Group Bindings dialog box
ms.assetid: ed642780-5350-438e-af73-b9ceab3f876d
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4d3d04692ac6576e76d2b630fb5cacb4f57db959
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66077855"
---
# <a name="measure-group-bindings-dialog-box-analysis-services---multidimensional-data"></a>Cuadro de diálogo Enlaces de grupo de medida (Analysis Services - Datos multidimensionales)
  Use el cuadro de diálogo **Enlaces de grupo de medida** para crear y modificar las relaciones directas entre los atributos que no son de granularidad de una dimensión de cubo y las columnas de un grupo de medida para una relación de dimensión regular, así como para especificar opciones de procesamiento de valores NULL para los atributos de una dimensión de cubo del cuadro de diálogo **Definir relación**.  
  
## <a name="options"></a>Opciones  
 **Tabla de grupos de medida**  
 Muestra el nombre de la tabla de hechos para el grupo de medida seleccionado.  
  
 **Atributos**  
 Muestra una cuadrícula de tablas de atributos y dimensiones. Seleccione un atributo para crear o modificar las propiedades de **Relación** del mismo. La cuadrícula contiene las columnas siguientes:  
  
|Opción|Definición|  
|------------|----------------|  
|**Nombre de atributo**|Muestra el nombre del atributo.|  
|**Tabla de dimensiones**|Muestra el nombre de la tabla de dimensiones en la que se basa el atributo.|  
  
 **Relación**  
 Muestra una cuadrícula de las relaciones existentes entre las columnas de las tablas de dimensiones para el atributo seleccionado y las columnas de las tablas de hechos para el grupo de medida seleccionado, así como la opción de procesamiento de valores NULL para la relación. La cuadrícula contiene las columnas siguientes:  
  
|Opción|Definición|  
|------------|----------------|  
|**Columnas de dimensión**|Muestra las columnas de la tabla de dimensiones en la que se basa el atributo seleccionado en **Atributos** .|  
|**Columnas de grupo de medida**|Seleccione **Heredado de la dimensión** para utilizar la relación de grupo de medida heredado de la dimensión o seleccione una columna de la tabla de hechos en la que se basa el grupo de medida para definir explícitamente una relación.|  
|**Procesamiento de valores null**|Seleccione una opción de procesamiento de valores NULL para el atributo. Para más información sobre las opciones de procesamiento de valores NULL, vea [Elemento NullProcessing &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/nullprocessing-element-assl).|  
  
## <a name="see-also"></a>Vea también  
 [Definir el cuadro de diálogo relación &#40;Analysis Services - datos multidimensionales&#41;](define-relationship-dialog-box-analysis-services-multidimensional-data.md)   
 [Diseñadores y cuadros de diálogo de Analysis Services &#40;datos multidimensionales&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)  
  
  
