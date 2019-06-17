---
title: Tabla (cuadro de diálogo origen de partición) de detalle del enlace (Analysis Services - datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.cubeeditor.partitions.partitiontableselection.f1
ms.assetid: 67d05389-81ae-4a6b-947b-986d37ec72b1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7f8ea36c8c3d49d4903379ed4450548fc760937a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66067867"
---
# <a name="table-binding-detail-partition-source-dialog-box-analysis-services---multidimensional-data"></a>Detalle del enlace de tablas (cuadro de diálogo Origen de la partición) (Analysis Services - Datos multidimensionales)
  Use la opción **Enlace de tablas** del cuadro de diálogo **Origen de la partición** para especificar la tabla de hechos que proporciona los datos para la partición. Puede mostrar este panel seleccionando **Enlace de tablas** en la opción **Tipo de enlace** del cuadro de diálogo **Origen de la partición** .  
  
## <a name="options"></a>Opciones  
 **Grupo de medida**  
 Muestra el grupo de medida para esta partición.  
  
 **Look in**  
 Seleccione el origen de datos o la vista del origen de datos que contiene las tablas de origen para la partición. La vista del origen de datos utilizada por el grupo de medida seleccionado es el valor seleccionado de manera predeterminada.  
  
 **Tablas de filtros**  
 Escriba la cadena que quiere usar para restringir las tablas mostradas en **Tablas disponibles**con el nombre de la tabla.  
  
 **Buscar tablas**  
 Seleccione esta opción para actualizar la lista de tablas de **Tablas disponibles**y restringir la lista si se ha especificado una cadena en **Tablas de filtros**.  
  
 **Tablas disponibles**  
 Haga clic en esta opción para seleccionar la tabla que se debe usar como tabla de origen para la partición.  
  
 Si no se especifica ningún filtro en **Tablas de filtros**, se enumeran todas las tablas del origen de datos o de la vista del origen de datos que se especificaron en **Buscar en** y cuya estructura es similar a la tabla de hechos utilizada por el grupo de medida especificado en **Grupo de medida** .  
  
 Si se especifica un filtro en **Tablas de filtros**, la lista se restringe aún más mediante la comparación del filtro con los nombres de tabla que cumplen los criterios mencionados anteriormente. Solo se mostrarán las tablas que contengan la cadena especificada en **Tablas de filtros** .  
  
## <a name="see-also"></a>Vea también  
 [Cuadro de diálogo origen de la partición &#40;Analysis Services - datos multidimensionales&#41;](partition-source-dialog-box-analysis-services-multidimensional-data.md)  
  
  
