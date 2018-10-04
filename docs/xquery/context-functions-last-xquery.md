---
title: Last (función de XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- last function [XQuery]
- fn:last function
ms.assetid: dc92086e-3b01-4b0b-9f54-3bbf306cf7ae
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: ab1240fd87ef49901ea17cad14523be8d86a45b8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47804613"
---
# <a name="context-functions---last-xquery"></a>Funciones de contexto: last (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve el número de elementos de la secuencia que se está procesando. En concreto, devuelve el índice entero del último elemento de la secuencia. El primer elemento de la secuencia tiene un valor de índice de 1.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
fn:last() as xs:integer  
```  
  
## <a name="remarks"></a>Comentarios  
 En SQL Server, **fn:Last()** sólo puede utilizarse en el contexto de un predicado dependiente del contexto. En concreto, solo se puede utilizar entre corchetes (`[ ]`).  
  
## <a name="examples"></a>Ejemplos  
 En este tema se proporciona ejemplos de XQuery con instancias XML almacenadas en varias **xml** columnas de tipo en la base de datos AdventureWorks.  
  
### <a name="a-using-the-last-xquery-function-to-retrieve-the-last-two-manufacturing-steps"></a>A. Usar la función last() de XQuery para recuperar los dos últimos pasos de fabricación  
 La consulta siguiente recupera los dos últimos pasos de fabricación de un modelo de producto determinado. El valor, el número de pasos de fabricación, devuelto por la **last()** función se usa en esta consulta para recuperar los dos últimos pasos de fabricación.  
  
```  
SELECT ProductModelID, Instructions.query('   
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
  <LastTwoManuSteps>  
   <Last-1Step>   
     { (/AWMI:root/AWMI:Location)[1]/AWMI:step[(last()-1)]/text() }  
   </Last-1Step>  
   <LastStep>   
     { (/AWMI:root/AWMI:Location)[1]/AWMI:step[last()]/text() }  
   </LastStep>  
  </LastTwoManuSteps>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 En la consulta anterior, el **last()** funcionando en /`/AWMI:root//AWMI:Location)[1]/AWMI:step[last()]` devuelve el número de pasos de fabricación. Este valor se utiliza para recuperar el último paso de fabricación de la ubicación de centro de trabajo.  
  
 El resultado es el siguiente:  
  
```  
ProductModelID Result    
-------------- -------------------------------------  
7      <LastTwoManuSteps>  
         <Last-1Step>  
            When finished, inspect the forms for defects per   
            Inspection Specification .  
         </Last-1Step>  
         <LastStep>Remove the frames from the tool and place them   
            in the Completed or Rejected bin as appropriate.  
         </LastStep>  
       </LastTwoManuSteps>  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones de XQuery con el tipo de datos xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
