---
title: Floor (función de XQuery) | Microsoft Docs
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
- floor function [XQuery]
- fn:floor function
ms.assetid: 4ace57dd-b66e-4b60-a2b9-a1b0f1a0831d
author: rothja
ms.author: jroth
ms.openlocfilehash: 1c27e432dc258b4d2b9d21bfe0ab28df8ee5b510
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67946531"
---
# <a name="numeric-values-functions---floor"></a>Funciones de valores numéricos: floor
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve el mayor número sin fracción que no supera el valor de su argumento. Si el argumento es una secuencia vacía, devuelve la secuencia vacía.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
fn:floor ($arg as numeric?) as numeric?  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Número al que se aplica la función.  
  
## <a name="remarks"></a>Observaciones  
 Si el tipo de *$arg* es uno de los tres tipos base numéricos, **xs: Float**, **xs: Double**o **xs: decimal**, el tipo de valor devuelto es el mismo que el tipo de *$arg* . Si el tipo de *$arg* es un tipo derivado de uno de los tipos numéricos, el tipo de valor devuelto es el tipo numérico base.  
  
 Si la entrada de las funciones FN: Floor, FN: Ceiling o FN: Round es **XDT: untypedAtomic**, datos sin tipo, se convierte implícitamente a **xs: Double**. Cualquier otro tipo genera un error estático.  
  
## <a name="examples"></a>Ejemplos  
 En este tema se proporcionan ejemplos de XQuery con instancias XML almacenadas en varias columnas de tipo **XML** en la base de datos de ejemplo AdventureWorks.  
  
 Puede usar el ejemplo de trabajo de la [función Ceiling (XQuery)](../xquery/numeric-values-functions-ceiling.md) para la función **Floor ()** de XQuery. Todo lo que tiene que hacer es sustituir la función **Ceiling ()** de la consulta por la función **Floor ()** .  
  
## <a name="implementation-limitations"></a>Limitaciones de la implementación  
 Éstas son las limitaciones:  
  
-   La función **Floor ()** asigna todos los valores enteros a XS: decimal.  
  
## <a name="see-also"></a>Consulte también  
 [Función Ceiling &#40;XQuery&#41;](../xquery/numeric-values-functions-ceiling.md)   
 [Función Round &#40;XQuery&#41;](../xquery/numeric-values-functions-round.md)   
 [Funciones de XQuery con el tipo de datos xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
