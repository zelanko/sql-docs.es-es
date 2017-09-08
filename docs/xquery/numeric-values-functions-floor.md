---
title: "Floor (función) (XQuery) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- floor function [XQuery]
- fn:floor function
ms.assetid: 4ace57dd-b66e-4b60-a2b9-a1b0f1a0831d
caps.latest.revision: 27
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4ebc7cd706986a4be284a0788b1976898fb5d313
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="numeric-values-functions---floor"></a>Funciones de valores numéricas - floor
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve el mayor número sin fracción que no supera el valor de su argumento. Si el argumento es una secuencia vacía, devuelve la secuencia vacía.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
fn:floor ($arg as numeric?) as numeric?  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Número al que se aplica la función.  
  
## <a name="remarks"></a>Comentarios  
 Si el tipo de *$arg* es uno de los tres tipos base numéricos, **xs: float**, **xs: Double**, o **xs: decimal**, el tipo de valor devuelto sea igual a la *$arg* tipo. Si el tipo de *$arg* es un tipo derivado de uno de los tipos numéricos, el tipo de valor devuelto es el tipo numérico base.  
  
 Si la entrada a las funciones fn: Floor, fn: Ceiling o fn: ROUND es **xdt: untypedAtomic**, datos sin tipo, se convierte implícitamente a **xs: Double**. Cualquier otro tipo genera un error estático.  
  
## <a name="examples"></a>Ejemplos  
 Este tema ofrecen ejemplos de XQuery con instancias XML almacenadas en varias **xml** columnas de tipo en la base de datos de ejemplo AdventureWorks.  
  
 Puede usar el ejemplo funcional de la [función ceiling (XQuery)](../xquery/numeric-values-functions-ceiling.md) para el **floor()** función de XQuery. Lo único que debe hacer es sustituir la **ceiling()** función en la consulta con la **floor()** función.  
  
## <a name="implementation-limitations"></a>Limitaciones de la implementación  
 Éstas son las limitaciones:  
  
-   El **floor()** función asigna todos los valores enteros a xs: decimal.  
  
## <a name="see-also"></a>Vea también  
 [Función CEILING &#40; XQuery &#41;](../xquery/numeric-values-functions-ceiling.md)   
 [Round (función) &#40; XQuery &#41;](../xquery/numeric-values-functions-round.md)   
 [Funciones de XQuery con el tipo de datos xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
