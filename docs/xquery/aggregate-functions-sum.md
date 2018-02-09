---
title: "SUM (función de XQuery) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/09/2017
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
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- sum function [XQuery]
- fn:sum function
ms.assetid: 12288f37-b54c-4237-b75e-eedc5fe8f96d
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 599080605291b48f30a40c85354ea5bb2f2320c6
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="aggregate-functions---sum"></a>Las funciones de agregado: suma
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve la suma de un flujo de números.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
fn:sum($arg as xdt:anyAtomicType*) as xdt:anyAtomicType  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Secuencia de valores atómicos cuya suma se va a calcular.  
  
## <a name="remarks"></a>Comentarios  
 Todos los tipos de valores atómicos que se pasan a **sum()** deben ser subtipos del mismo tipo base. Los tipos base aceptados son los tres tipos numéricos base integrados o xdt:untypedAtomic. Los valores del tipo xdt:untypedAtomic se convierten a xs:double. Si hay una combinación de estos tipos, o si se pasan otros valores de otros tipos, se produce un error estático.  
  
 El resultado de **sum()** recibe el tipo base de los tipos pasados como xs: double en el caso de xdt: untypedAtomic, incluso si la entrada, opcionalmente, es una secuencia vacía. Si se trata de una entrada vacía estática, el resultado es 0 con el tipo estático y dinámico xs:integer.  
  
 El **sum()** función devuelve la suma de los valores numéricos. Si no se puede convertir un valor xdt: untypedAtomic a xs: Double, el valor se omite en la secuencia de entrada, *$arg*. Si la entrada es una secuencia vacía calculada dinámicamente, se devuelve el valor 0 del tipo base utilizado.  
  
 La función devuelve un error en tiempo de ejecución cuando se produce una excepción por desbordamiento o por valores fuera del intervalo.  
  
## <a name="examples"></a>Ejemplos  
 Este tema ofrecen ejemplos de XQuery con instancias XML almacenadas en varias **xml** escriba columnas en la [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] base de datos.  
  
### <a name="a-using-the-sum-xquery-function-to-find-the-total-combined-number-of-labor-hours-for-all-work-center-locations-in-the-manufacturing-process"></a>A. Utilizar la función sum() de XQuery para calcular el número total de horas de trabajo de todos los centros de trabajo del proceso de fabricación  
 La consulta siguiente averigua el número total de horas de trabajo para todos los centros de trabajo del proceso de fabricación de todos los modelos de producto para los que se almacenan instrucciones de fabricación.  
  
```  
SELECT Instructions.query('         
   declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";         
  <ProductModel PMID= "{ sql:column("Production.ProductModel.ProductModelID") }"         
  ProductModelName = "{ sql:column("Production.ProductModel.Name") }" >         
   <TotalLaborHrs>         
     { sum(//AWMI:Location/@LaborHours) }         
   </TotalLaborHrs>         
 </ProductModel>         
    ') as Result         
FROM Production.ProductModel         
WHERE Instructions is not NULL         
```  
  
 El resultado parcial es el siguiente.  
  
```  
<ProductModel PMID="7" ProductModelName="HL Touring Frame">  
   <TotalLaborHrs>12.75</TotalLaborHrs>  
</ProductModel>  
<ProductModel PMID="10" ProductModelName="LL Touring Frame">  
  <TotalLaborHrs>13</TotalLaborHrs>  
</ProductModel>  
...  
```  
  
 En lugar de obtener el resultado como XML, puede escribir la consulta de manera que genere resultados relacionales, como la consulta siguiente:  
  
```  
SELECT ProductModelID,         
        Name,         
        Instructions.value('declare namespace   
      AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";         
    sum(//AWMI:Location/@LaborHours)', 'float') as TotalLaborHours         
FROM Production.ProductModel         
WHERE Instructions is not NULL          
```  
  
 Éste es un resultado parcial:  
  
```  
ProductModelID Name                 TotalLaborHours         
-------------- -------------------------------------------------  
7              HL Touring Frame           12.75                   
10             LL Touring Frame           13                      
43             Touring Rear Wheel         3                       
...  
```  
  
### <a name="implementation-limitations"></a>Limitaciones de la implementación  
 Éstas son las limitaciones:  
  
-   Solo la versión de argumento único de **sum()** se admite.  
  
-   Si la entrada es una secuencia vacía calculada dinámicamente, se devuelve el valor 0 del tipo base utilizado, en lugar del tipo xs:integer.  
  
-   El **sum()** función asigna todos los enteros a xs: decimal.  
  
-   El **sum()** no se admite la función de valores de tipo xs: Duration.  
  
-   No se admiten las secuencias que mezclan tipos en límites de tipo base.  
  
-   sum((xs:double(“INF”), xs:double(“-INF”))) genera un error de dominio.  
  
## <a name="see-also"></a>Vea también  
 [Funciones de XQuery con el tipo de datos xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
