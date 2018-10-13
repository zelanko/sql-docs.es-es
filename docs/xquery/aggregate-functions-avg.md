---
title: AVG (función de XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:avg function
- avg function [XQuery]
ms.assetid: 0cc60267-3c56-4a88-8ad7-bb07f0255d56
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a80c7f690a4b24ef82cb3da34dea50c98cf836f4
ms.sourcegitcommit: 08b3de02475314c07a82a88c77926d226098e23f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/12/2018
ms.locfileid: "49119662"
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
 Todos los tipos de valores atomizados que se pasan a **avg()** tiene que ser un subtipo de exactamente uno de los tres tipos numéricos base integrados o xdt: untypedAtomic. No se pueden mezclar. Los valores de tipo xdt:untypedAtomic se tratan como xs:double. El resultado de **avg()** recibe el tipo base de los tipos pasados, como xs: double en el caso de xdt: untypedAtomic.  
  
 Si la entrada está estáticamente vacía, se considera implícitamente vacía y se produce un error estático.  
  
 El **avg()** función devuelve el promedio de los números calculados. Por ejemplo:  
  
 **SUM (** *$arg* **) div count (** *$arg* **)**  
  
 Si *$arg* es una secuencia vacía, se devuelve una secuencia vacía.  
  
 Si no se puede convertir un valor xdt: untypedAtomic a xs: Double, se descarta el valor en la secuencia de entrada *$arg*.  
  
 En los demás casos, la función devuelve un error estático.  
  
## <a name="examples"></a>Ejemplos  
 En este tema se proporciona ejemplos de XQuery con instancias XML almacenadas en varias **xml** columnas de tipo en la base de datos AdventureWorks.  
  
### <a name="a-using-the-avg-xquery-function-to-find-work-center-locations-in-the-manufacturing-process-in-which-labor-hours-are-greater-than-the-average-for-all-work-center-locations"></a>A. Utilizar la función avg() de XQuery para buscar los centros de trabajo del proceso de fabricación cuyas horas de trabajo son superiores al promedio de todos los centros de trabajo  
 Puede volver a escribir la consulta proporcionada en [min (función de XQuery)](../xquery/aggregate-functions-min.md) para usar el **avg()** función.  
  
## <a name="implementation-limitations"></a>Limitaciones de la implementación  
 Éstas son las limitaciones:  
  
-   El **avg()** función asigna todos los enteros a xs: decimal.  
  
-   El **avg()** no se admite la función con valores de tipo xs: Duration.  
  
-   No se admiten las secuencias que mezclan tipos en límites de tipo base.  
  
## <a name="see-also"></a>Vea también  
 [Funciones de XQuery con el tipo de datos xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
