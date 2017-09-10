---
title: "Atomización (XQuery) | Documentos de Microsoft"
ms.custom: 
ms.date: 08/01/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- XQuery, atomization
- atomization [XQuery]
ms.assetid: e3d7cf2f-c6fb-43c2-8538-4470a6375af5
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5251917c137d6a37b18a47659e66ed3ea9154e36
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="atomization-xquery"></a>Atomización (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La atomización es un proceso que consiste en extraer el valor con tipo de un elemento. Este proceso se produce en determinadas circunstancias. Algunos de los operadores XQuery, como los aritméticos y los de comparación, dependen de este proceso. Por ejemplo, al aplicar operadores aritméticos directamente a los nodos, el valor con tipo de un nodo se recupera primero invocando implícitamente la [función datos](../xquery/data-accessor-functions-data-xquery.md). De esta manera, el valor atómico se pasa al operador aritmético como un operando.  
  
 Por ejemplo, la consulta siguiente devuelve el total de los atributos LaborHours. En este caso, **data()** se aplica implícitamente a los nodos de atributo.  
  
```  
declare @x xml  
set @x='<ROOT><Location LID="1" SetupTime="1.1" LaborHours="3.3" />  
<Location LID="2" SetupTime="1.0" LaborHours="5" />  
<Location LID="3" SetupTime="2.1" LaborHours="4" />  
</ROOT>'  
-- data() implicitly applied to the attribute node sequence.  
SELECT @x.query('sum(/ROOT/Location/@LaborHours)')  
```  
  
 Aunque no es necesario, puede especificar explícitamente el **data()** función:  
  
```  
SELECT @x.query('sum(data(ROOT/Location/@LaborHours))')  
```  
  
 Otro ejemplo de atomización implícita se produce al utilizar operadores aritméticos. El  **+**  operador requiere valores atómicos y **data()** se aplica implícitamente para recuperar el valor atómico del atributo LaborHours. La consulta se especifica en la columna Instructions de la **xml** tipo en la tabla ProductModel. La consulta siguiente devuelve el atributo LaborHours tres veces. Respecto a la consulta, observe lo siguiente:  
  
-   Al construir el atributo OrigninalLaborHours, la atomización se aplica implícitamente a la secuencia singleton devuelta por (`$WC/@LaborHours`). El valor con tipo del atributo LaborHours se asigna a OrigninalLaborHours.  
  
-   Al construir el atributo UpdatedLaborHoursV1, el operador aritmético requiere valores atómicos. Por lo tanto, **data()** se aplica implícitamente al atributo LaborHours devuelto por (`$WC/@LaborHours`). A continuación, se le agrega el valor atómico 1. La creación del atributo UpdatedLaborHoursV2 muestra la aplicación explícita de **data()**, pero no es necesario.  
  
```  
SELECT Instructions.query('  
     declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
for $WC in /AWMI:root/AWMI:Location[1]  
        return  
            <WC OriginalLaborHours = "{ $WC/@LaborHours }"  
                UpdatedLaborHoursV1 = "{ $WC/@LaborHours + 1 }"   
                UpdatedLaborHoursV2 = "{ data($WC/@LaborHours) + 1 }" >  
            </WC>') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
 El resultado es el siguiente:  
  
```  
<WC OriginalLaborHours="2.5"   
    UpdatedLaborHoursV1="3.5"   
    UpdatedLaborHoursV2="3.5" />  
```  
  
 La atomización da lugar a una instancia de tipo simple, un conjunto vacío o un error de tipo estático.  
  
 La atomización también se produce en parámetros de la expresión de comparación pasados a funciones, valores devueltos por funciones, **cast()** expresiones y expresiones de orden pasadas en el orden por cláusula.  
  
## <a name="see-also"></a>Vea también  
 [Conceptos básicos de XQuery](../xquery/xquery-basics.md)   
 [Expresiones de comparación &#40; XQuery &#41;](../xquery/comparison-expressions-xquery.md)   
 [Funciones de XQuery con el tipo de datos xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  

