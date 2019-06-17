---
title: + (Concatenar) (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- concatenation [Integration Services]
- + (concatenate operator)
- concatenate operator (+)
ms.assetid: 0fed6334-7a4f-42dc-a611-191fcaa0e443
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 288e4aedc6112640aa511712ad90912b1d41b2fa
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62769378"
---
# <a name="-concatenate-ssis-expression"></a>+ (Concatenar) (expresión de SSIS)
  Concatena dos expresiones en una expresión.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
character_expression1 + character_expression2  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression1, expression2*  
 Cualquier expresión válida con tipo de datos DT_STR, DT_WSTR, DT_TEXT, DT_NTEXT o DT_IMAGE.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_WSTR  
  
## <a name="remarks"></a>Comentarios  
 La expresión puede usar los tipos de datos DT_STR y DT_WSTR, o uno de los dos.  
  
 La concatenación de los tipos de datos DT_STR y DT_WSTR devuelve un resultado de tipo DT_WSTR. La longitud de la cadena es la suma de las longitudes de las cadenas originales expresadas en caracteres.  
  
 Solo se pueden concatenar datos con los tipos de datos de cadena DT_STR y DT_WSTR o con los tipos de datos de bloque de objetos binarios grandes (BLOB) DT_TEXT, DT_NTEXT y DT_IMAGE. Los otros tipos de datos deben convertirse explícitamente en uno de estos tipos de datos antes de que se produzca la concatenación. Para más información sobre conversiones válidas entre tipos de datos, vea [Conversión &#40;expresión de SSIS&#41;](cast-ssis-expression.md).  
  
 Ambas expresiones deben tener el mismo tipo de datos o una expresión debe poder convertirse implícitamente al tipo de datos de la otra expresión. Por ejemplo, si se concatena la cadena "Order date is " y la columna **OrderDate** , los valores de **OrderDate** se convierten implícitamente a un tipo de datos de cadena. Para concatenar dos valores numéricos, ambos valores deben convertirse explícitamente a un tipo de datos de cadena.  
  
 Una concatenación puede utilizar solo un tipo de datos BLOB: DT_TEXT, DT_NTEXT o DT_IMAGE.  
  
 Si alguno de los elementos es NULL, el resultado será NULL.  
  
 Los literales de cadena deben escribirse entre comillas.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo concatena los valores de las columnas **FirstName** y **LastName** e inserta un espacio entre ellos.  
  
```  
FirstName + ' ' + LastName  
```  
  
 En este ejemplo se concatenan las variables **ZIPCode** y **ZIPCode+4**. Ambas variables tienen un tipo de datos de cadena. **ZIPCode+4** debe escribirse entre corchetes porque el nombre de la variable incluye el carácter +.  
  
```  
@ZIPCcode + "-" + @[ZipCode+4]  
```  
  
## <a name="see-also"></a>Vea también  
 [Precedencia y capacidad de asociación de operadores](operator-precedence-and-associativity.md)   
 [Operadores &#40;expresión de SSIS&#41;](operators-ssis-expression.md)  
  
  
