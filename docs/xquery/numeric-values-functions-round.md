---
title: Round (función) (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:round function
- round function [XQuery]
ms.assetid: 320b572f-bd5b-4055-95a6-dec5718c0041
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8c0b5847cb5d4b4d6643edceadbd4d95cec5f152
ms.sourcegitcommit: 0f7cf9b7ab23df15624d27c129ab3a539e8b6457
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2018
ms.locfileid: "51292741"
---
# <a name="numeric-values-functions---round"></a>Funciones de valores numéricos: round
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve el número que no tiene una parte fraccionaria más próxima al valor del argumento. Si hay más de un número con esta característica, se devuelve el más próximo al infinito positivo. Por ejemplo:  
  
 Si el argumento es la 2.5, **round()** devuelve 3.  
  
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
 Si el tipo de *$arg* es uno de los tres tipos bases numéricos, **xs: float**, **xs: Double**, o **xs: decimal**, el tipo de valor devuelto es el mismo que el *$arg* tipo. Si el tipo de *$arg* es un tipo derivado de uno de los tipos numéricos, el tipo de valor devuelto es el tipo base numérico.  
  
 Si como entrada para el **fn: Floor**, **fn**, o **fn: Round** functions es **xdt: untypedAtomic**, datos sin tipo, se convierte implícitamente a **xs: Double**.  
  
 Cualquier otro tipo genera un error estático.  
  
## <a name="examples"></a>Ejemplos  
 En este tema se proporciona ejemplos de XQuery con instancias XML almacenadas en varias **xml** columnas de tipo en la base de datos AdventureWorks.  
  
 Puede usar el ejemplo funcional de la [función ceiling (XQuery)](../xquery/numeric-values-functions-ceiling.md) para el **round()** función de XQuery. Lo único que debe hacer es sustituir el **ceiling()** función en la consulta con el **round()** función.  
  
## <a name="implementation-limitations"></a>Limitaciones de la implementación  
 Éstas son las limitaciones:  
  
-   El **round()** función asigna valores enteros a xs: decimal.  
  
-   El **round()** función de los valores xs: Double y xs: float entre - 0.5e0 y - 0e0 a 0e0 en lugar de - 0e0.  
  
## <a name="see-also"></a>Vea también  
 [Función FLOOR &#40;XQuery&#41;](../xquery/numeric-values-functions-floor.md)   
 [Función CEILING &#40;XQuery&#41;](../xquery/numeric-values-functions-ceiling.md)  
  
  
