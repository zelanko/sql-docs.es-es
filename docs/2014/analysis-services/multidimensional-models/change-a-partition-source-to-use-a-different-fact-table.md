---
title: Cambiar el origen de una partición para usar una tabla de hechos diferente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- fact tables [Analysis Services]
- partitions [Analysis Services], fact tables
ms.assetid: 5508312f-8e46-4802-9362-6688ca03d098
author: minewiskan
ms.author: owend
ms.openlocfilehash: 0063a6023d769dc6dccd616655d10e0bd3c65a98
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84537176"
---
# <a name="change-a-partition-source-to-use-a-different-fact-table"></a>Cambiar el origen de una partición para usar una tabla de hechos diferente
  Cuando se crea una partición para un cubo, se puede usar una tabla de hechos diferente. Las tablas diferentes pueden proceder de una única vista del origen de datos, de diferentes vistas del origen de datos o de diferentes orígenes de datos. Una vista del origen de datos también puede contener tablas diferentes de más de un origen de datos.  
  
 Todas las tablas de hechos y dimensiones correspondientes a las particiones de un cubo deben tener la misma estructura que la tabla de hechos y las dimensiones del cubo. Por ejemplo, varias tablas de hechos pueden tener la misma estructura pero contener datos de años distintos o de líneas de productos diferentes.  
  
 La tabla de hechos se especifica en la página **Especificar información de origen** del Asistente para particiones. En esta página, en el grupo Origen de la partición que hay al lado de **Buscar en**, especifique un origen de datos o una vista del origen de datos en la que se debe buscar. A continuación, haga clic en **Buscar tablas**y, a continuación, en **Tablas disponibles**, seleccione la tabla que desea usar.  
  
 Cuando utilice tablas de hechos diferentes, asegúrese de que no hay datos duplicados en las distintas particiones. Por ejemplo, si una tabla de hechos contiene únicamente transacciones del año 2012 y otra solo contiene transacciones correspondientes a 2013, ambas contienen datos independientes. Igualmente son independientes las tablas de hechos correspondientes a líneas de productos o a áreas geográficas distintas.  
  
 Es posible, pero no se recomienda, utilizar diferentes tablas de hechos que contengan datos duplicados. En este caso, debe utilizar filtros en las particiones para asegurarse de que los datos empleados por una partición no serán utilizados por ninguna otra. Para obtener más información, vea [Crear y administrar una partición local &#40;Analysis Services&#41;](create-and-manage-a-local-partition-analysis-services.md).  
  
## <a name="see-also"></a>Consulte también  
 [Crear y administrar una partición local &#40;Analysis Services&#41;](create-and-manage-a-local-partition-analysis-services.md)  
  
  
