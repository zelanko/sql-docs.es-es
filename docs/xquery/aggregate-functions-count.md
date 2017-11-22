---
title: "Count, función (XQuery) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- fn:count function
- count function [XQuery]
ms.assetid: a9f7131f-23e1-4d4d-a36c-180447543926
caps.latest.revision: "27"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b868f88df37c18f3790cc1c9c5cd5b4ddd5fa623
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="aggregate-functions---count"></a>Funciones de agregado: count
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve el número de elementos incluidos en la secuencia especificada por *$arg*.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
fn:count($arg as item()*) as xs:integer  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Elementos que se deben contar.  
  
## <a name="remarks"></a>Comentarios  
 Devuelve 0 si *$arg* es una secuencia vacía.  
  
## <a name="examples"></a>Ejemplos  
 Este tema ofrecen ejemplos de XQuery con instancias XML almacenadas en varias **xml** columnas de tipo en la base de datos de AdventureWorks.  
  
### <a name="a-using-the-count-xquery-function-to-count-the-number-of-work-center-locations-in-the-manufacturing-of-a-product-model"></a>A. Utilizar la función count() de XQuery para contar el número de centros de trabajo en la fabricación de un modelo de producto  
 La consulta siguiente cuenta el número de centros de trabajo que participan en el proceso de fabricación de un modelo de producto (ProductModelID=7).  
  
```  
SELECT Production.ProductModel.ProductModelID,   
       Production.ProductModel.Name,   
       Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
       <NoOfWorkStations>  
          { count(/AWMI:root/AWMI:Location) }  
       </NoOfWorkStations>  
') as WorkCtrCount  
FROM Production.ProductModel  
WHERE Production.ProductModel.ProductModelID=7  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   El **espacio de nombres** palabra clave en [prólogo de XQuery](../xquery/modules-and-prologs-xquery-prolog.md) define un prefijo de espacio de nombres. El prefijo se utiliza, a continuación, en el cuerpo de XQuery.  
  
-   La consulta construye una instancia XML que incluye el elemento <`NoOfWorkStations`>.  
  
-   El **count()** funcionar en los recuentos de cuerpo de XQuery el número de <`Location`> elementos.  
  
 El resultado es el siguiente:  
  
```  
ProductModelID   Name                 WorkCtrCount       
-------------- ---------------------------------------------------  
7             HL Touring Frame  <NoOfWorkStations>6</NoOfWorkStations>     
```  
  
 También puede construir la instancia XML de modo que incluya el identificador y el nombre del modelo de producto, tal y como se muestra en la consulta siguiente:  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
       <NoOfWorkStations  
             ProductModelID= "{ sql:column("Production.ProductModel.ProductModelID") }"   
             ProductModelName = "{ sql:column("Production.ProductModel.Name") }" >  
          { count(/AWMI:root/AWMI:Location) }  
       </NoOfWorkStations>  
') as WorkCtrCount  
FROM Production.ProductModel  
WHERE Production.ProductModel.ProductModelID= 7  
```  
  
 El resultado es el siguiente:  
  
```  
<NoOfWorkStations ProductModelID="7"   
                  ProductModelName="HL Touring Frame">6</NoOfWorkStations>  
```  
  
 En lugar de la instancia XML, puede devolver estos valores con un tipo distinto de xml, tal y como se muestra en la consulta siguiente. La consulta utiliza la [método value() (tipo de datos xml)](../t-sql/xml/value-method-xml-data-type.md) para recuperar el recuento de centros de trabajo.  
  
```  
SELECT  ProductModelID,   
        Name,   
        Instructions.value('declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
           count(/AWMI:root/AWMI:Location)', 'int' ) as WorkCtrCount  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 El resultado es el siguiente:  
  
```  
ProductModelID    Name            WorkCtrCount  
-------------- ---------------------------------  
7              HL Touring Frame        6     
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones de XQuery con el tipo de datos xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
