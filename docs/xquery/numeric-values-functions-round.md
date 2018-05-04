---
title: Round (función) (XQuery) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.service: ''
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- fn:round function
- round function [XQuery]
ms.assetid: 320b572f-bd5b-4055-95a6-dec5718c0041
caps.latest.revision: 29
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a5626f5e882d7ca9f300b0ec5c2dae50d2f426ce
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="numeric-values-functions---round"></a>Funciones de valores numéricas - de ida y vuelta
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve el número que no tiene una parte fraccionaria más próxima al valor del argumento. Si hay más de un número con esta característica, se devuelve el más próximo al infinito positivo. Por ejemplo:  
  
 Si el argumento es 2.5, **round()** devuelve 3.  
  
 Si el argumento es 2.4999, **round()** devuelve 2.  
  
 Si el argumento es -2,5, **round()** devuelve -2.  
  
 Si el argumento es una secuencia vacía, **round()** devuelve una secuencia vacía.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
fn:round ( $arg as numeric?) as numeric?  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Número al que se aplica la función.  
  
## <a name="remarks"></a>Comentarios  
 Si el tipo de *$arg* es uno de los tres tipos base numéricos, **xs: float**, **xs: Double**, o **xs: decimal**, el tipo de valor devuelto sea igual a la *$arg* tipo. Si el tipo de *$arg* es un tipo derivado de uno de los tipos numéricos, el tipo de valor devuelto es el tipo numérico base.  
  
 Si como entrada para la **fn: Floor**, **fn**, o **fn: Round** funciona **xdt: untypedAtomic**, datos sin tipo, se convierte implícitamente a **xs: Double**.  
  
 Cualquier otro tipo genera un error estático.  
  
## <a name="examples"></a>Ejemplos  
 En este tema se ofrece ejemplos de XQuery con instancias XML almacenadas en varias **xml** columnas de tipo en la base de datos de AdventureWorks.  
  
 Puede usar el ejemplo funcional de la [función ceiling (XQuery)](../xquery/numeric-values-functions-ceiling.md) para el **round()** función de XQuery. Lo único que debe hacer es sustituir la **ceiling()** función en la consulta con la **round()** función.  
  
## <a name="implementation-limitations"></a>Limitaciones de la implementación  
 Éstas son las limitaciones:  
  
-   El **round()** función asigna valores enteros a xs: decimal.  
  
-   El **round()** función de valores xs: Double y xs: float entre - 0.5e0 y - 0e0 a 0e0 en lugar de - 0e0.  
  
## <a name="see-also"></a>Vea también  
 [Floor (función) &#40;XQuery&#41;](../xquery/numeric-values-functions-floor.md)   
 [Función CEILING &#40;XQuery&#41;](../xquery/numeric-values-functions-ceiling.md)  
  
  
