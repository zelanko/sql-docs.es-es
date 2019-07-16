---
title: Max (función de XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- max function [XQuery]
- fn:max function
ms.assetid: 5ee625c0-044a-4cda-b210-02b64e619d65
author: rothja
ms.author: jroth
ms.openlocfilehash: e47539a350a2918ef24c47e3c1eca270d4aeb72e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985953"
---
# <a name="aggregate-functions---max"></a>Funciones de agregado: max
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve de una secuencia de valores atómicos, *$arg*, el único elemento cuyo valor es mayor que el de todos los demás.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
fn:max($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Secuencia de valores atómicos a partir de la cual se va a devolver el valor máximo.  
  
## <a name="remarks"></a>Comentarios  
 Todos los tipos de valores atomizados que se pasan a **max()** deben ser subtipos del mismo tipo base. Tipos base aceptados son los tipos que admiten la **gt** operación. Entre estos tipos se incluyen los tres tipos base numéricos integrados, los tipos base de fecha y hora, xs:string, xs:boolean y xdt:untypedAtomic. Los valores del tipo xdt:untypedAtomic se convierten a xs:double. Si es una combinación de estos tipos, o si se pasan otros valores de otros tipos, se produce un error estático.  
  
 El resultado de **max()** recibe el tipo base de los tipos pasados, como xs: double en el caso de xdt: untypedAtomic. Si la entrada está estáticamente vacía, se considera implícitamente vacía y se produce un error estático.  
  
 El **max()** función devuelve un valor de la secuencia que es mayor que cualquier otro en la secuencia de entrada. En el caso de los valores xs:string, se utiliza la intercalación de puntos de código Unicode predeterminada. Si no se puede convertir un valor xdt: untypedAtomic a xs: Double, el valor se omite en la secuencia de entrada *$arg*. Si la entrada es una secuencia vacía calculada dinámicamente, se devolverá la secuencia vacía.  
  
## <a name="examples"></a>Ejemplos  
 En este tema se proporciona ejemplos de XQuery con instancias XML almacenadas en varias **xml** escriba columnas en el [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] base de datos.  
  
### <a name="a-using-the-max-xquery-function-to-find-work-center-locations-in-the-manufacturing-process-that-have-the-most-labor-hours"></a>A. Utilizar la función max() de XQuery para buscar las ubicaciones de centro de trabajo del proceso de fabricación que tienen más horas de trabajo  
 La consulta proporcionada en [min (función de XQuery)](../xquery/aggregate-functions-min.md) puede reescribirse para utilizar el **max()** función.  
  
## <a name="implementation-limitations"></a>Limitaciones de la implementación  
 Éstas son las limitaciones:  
  
-   El **max (** ) función asigna todos los enteros a xs: decimal.  
  
-   El **max()** no se admite la función con valores de tipo xs: Duration.  
  
-   No se admiten las secuencias que mezclan tipos en límites de tipo base.  
  
-   No se admite la opción sintáctica que proporciona una intercalación.  
  
## <a name="see-also"></a>Vea también  
 [Funciones de XQuery con el tipo de datos xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
