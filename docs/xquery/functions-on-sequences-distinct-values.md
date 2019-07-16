---
title: DISTINCT-values, función (XQuery) | Microsoft Docs
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
- distinct-values function
- fn:distinct-values function
ms.assetid: f4c2bb53-2bec-4f1a-9c00-cf997fb7ae5b
author: rothja
ms.author: jroth
ms.openlocfilehash: d2f856c9b351c776651f08e66f90c7f567a5dcfc
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68223733"
---
# <a name="functions-on-sequences---distinct-values"></a>Funciones usadas en secuencias: distinct-values
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita valores duplicados de la secuencia especificada por *$arg*. Si *$arg* es una secuencia vacía, la función devuelve una secuencia vacía.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
fn:distinct-values($arg as xdt:anyAtomicType*) as xdt:anyAtomicType*  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Secuencia de valores atómicos.  
  
## <a name="remarks"></a>Comentarios  
 Todos los tipos de valores atomizados que se pasan a **distinct-values()** deben ser subtipos del mismo tipo base. Tipos base aceptados son los tipos que admiten la **eq** operación. Entre estos tipos se incluyen los tres tipos base numéricos integrados, los tipos base de fecha y hora, xs:string, xs:boolean y xdt:untypedAtomic. Los valores de tipo xdt:untypedAtomic se convierten en xs:string. Si hay un mezcla de estos tipos, o si se pasan otros valores de otros tipos, se produce un error estático.  
  
 El resultado de **distinct-values()** recibe el tipo base de los tipos pasados, como xs: String en el caso de xdt: untypedAtomic, con la cardinalidad original. Si la entrada está estáticamente vacía, se considera implícitamente vacía y se produce un error estático.  
  
 Los valores de tipo xs:string se comparan con la intercalación de punto de código Unicode predeterminada de XQuery.  
  
## <a name="examples"></a>Ejemplos  
 En este tema se proporciona ejemplos de XQuery con instancias XML almacenadas en varias **xml** columnas de tipo en la base de datos AdventureWorks.  
  
### <a name="a-using-the-distinct-values-function-to-remove-duplicate-values-from-the-sequence"></a>A. Usar la función distinct-values() para quitar valores duplicados de la secuencia  
 En este ejemplo, una instancia XML que contiene los números de teléfono se asigna a un **xml** variable de tipo. La expresión XQuery especificada para esta variable utiliza la **distinct-values()** función para compilar una lista de números de teléfono que no contienen duplicados.  
  
```  
declare @x xml  
set @x = '<PhoneNumbers>  
 <Number>111-111-1111</Number>  
 <Number>111-111-1111</Number>  
 <Number>222-222-2222</Number>  
</PhoneNumbers>'  
-- 1st select  
select @x.query('  
  distinct-values( data(/PhoneNumbers/Number) )  
') as result  
```  
  
 Éste es el resultado:  
  
```  
111-111-1111 222-222-2222    
```  
  
 En la consulta siguiente, se pasa una secuencia de números (1, 1, 2) a la **distinct-values()** función. A continuación, la función quita el duplicado de la secuencia y devuelve los otros dos valores.  
  
```  
declare @x xml  
set @x = ''  
select @x.query('  
  distinct-values((1, 1, 2))  
') as result  
```  
  
 La consulta devuelve 1 y 2.  
  
### <a name="implementation-limitations"></a>Limitaciones de la implementación  
 Éstas son las limitaciones:  
  
-   El **distinct-values()** función asigna valores enteros a xs: decimal.  
  
-   El **distinct-values()** función solo admite los tipos mencionados anteriormente y no admite la mezcla de tipos base.  
  
-   El **distinct-values()** no se admite la función valores xs: Duration.  
  
-   No se admite la opción sintáctica que proporciona una intercalación.  
  
## <a name="see-also"></a>Vea también  
 [Funciones de XQuery con el tipo de datos xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
