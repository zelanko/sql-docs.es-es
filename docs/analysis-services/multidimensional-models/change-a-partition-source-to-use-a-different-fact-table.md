---
title: Cambiar el origen de una partición para usar una tabla de hechos diferentes | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 53609a1c252455f8372fd43b6a1323e93f0b3024
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62991777"
---
# <a name="change-a-partition-source-to-use-a-different-fact-table"></a>Cambiar el origen de una partición para usar una tabla de hechos diferente
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Cuando se crea una partición para un cubo, se puede usar una tabla de hechos diferente. Las tablas diferentes pueden proceder de una única vista del origen de datos, de diferentes vistas del origen de datos o de diferentes orígenes de datos. Una vista del origen de datos también puede contener tablas diferentes de más de un origen de datos.  
  
 Todas las tablas de hechos y dimensiones correspondientes a las particiones de un cubo deben tener la misma estructura que la tabla de hechos y las dimensiones del cubo. Por ejemplo, varias tablas de hechos pueden tener la misma estructura pero contener datos de años distintos o de líneas de productos diferentes.  
  
 La tabla de hechos se especifica en la página **Especificar información de origen** del Asistente para particiones. En esta página, en el grupo Origen de la partición que hay al lado de **Buscar en**, especifique un origen de datos o una vista del origen de datos en la que se debe buscar. A continuación, haga clic en **Buscar tablas**y, a continuación, en **Tablas disponibles**, seleccione la tabla que desea usar.  
  
 Cuando utilice tablas de hechos diferentes, asegúrese de que no hay datos duplicados en las distintas particiones. Por ejemplo, si una tabla de hechos contiene únicamente transacciones del año 2012 y otra solo contiene transacciones correspondientes a 2013, ambas contienen datos independientes. Igualmente son independientes las tablas de hechos correspondientes a líneas de productos o a áreas geográficas distintas.  
  
 Es posible, pero no se recomienda, utilizar diferentes tablas de hechos que contengan datos duplicados. En este caso, debe utilizar filtros en las particiones para asegurarse de que los datos empleados por una partición no serán utilizados por ninguna otra. Para más información, vea [Crear y administrar una partición local &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/create-and-manage-a-local-partition-analysis-services.md).  
  
## <a name="see-also"></a>Vea también  
 [Crear y administrar una partición local &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/create-and-manage-a-local-partition-analysis-services.md)  
  
  
