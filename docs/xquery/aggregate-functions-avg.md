---
title: "AVG (función de XQuery) | Documentos de Microsoft"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:avg function
- avg function [XQuery]
ms.assetid: 0cc60267-3c56-4a88-8ad7-bb07f0255d56
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ee1d24bc4b28b7a041baa42ac829424e5daa6f8b
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="aggregate-functions---avg"></a>Funciones de agregado: avg
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el promedio de una secuencia de números.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
fn:avg($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Secuencia de valores atómicos cuyo promedio se va a calcular.  
  
## <a name="remarks"></a>Comentarios  
 Todos los tipos de valores atómicos que se pasan a **avg()** tiene que ser un subtipo de uno de los tres tipos numéricos base integrados o xdt: untypedAtomic. No se pueden mezclar. Los valores de tipo xdt:untypedAtomic se tratan como xs:double. El resultado de **avg()** recibe el tipo base de los tipos pasados, como xs: double en el caso de xdt: untypedAtomic.  
  
 Si se trata de una entrada vacía estática, se presupone que está vacía y se genera un error estático.  
  
 El **avg()** función devuelve el promedio de los números calculados. Por ejemplo:  
  
 **SUM (** *$arg* **) div count (** *$arg* **)**  
  
 Si *$arg* es una secuencia vacía, se devuelve una secuencia vacía.  
  
 Si no se puede convertir un valor xdt: untypedAtomic a xs: Double, se descarta el valor en la secuencia de entrada, *$arg*.  
  
 En los demás casos, la función devuelve un error estático.  
  
## <a name="examples"></a>Ejemplos  
 Este tema ofrecen ejemplos de XQuery con instancias XML almacenadas en varias **xml** columnas de tipo en la base de datos de AdventureWorks.  
  
### <a name="a-using-the-avg-xquery-function-to-find-work-center-locations-in-the-manufacturing-process-in-which-labor-hours-are-greater-than-the-average-for-all-work-center-locations"></a>A. Utilizar la función avg() de XQuery para buscar los centros de trabajo del proceso de fabricación cuyas horas de trabajo son superiores al promedio de todos los centros de trabajo  
 Puede volver a escribir la consulta proporcionada en [min (función) (XQuery)](../xquery/aggregate-functions-min.md) para usar el **avg()** (función).  
  
## <a name="implementation-limitations"></a>Limitaciones de la implementación  
 Éstas son las limitaciones:  
  
-   El **avg()** función asigna todos los enteros a xs: decimal.  
  
-   El **avg()** no se admite la función de valores de tipo xs: Duration.  
  
-   No se admiten las secuencias que mezclan tipos en límites de tipo base.  
  
## <a name="see-also"></a>Vea también  
 [Funciones de XQuery con el tipo de datos xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
