---
title: Usar el modo AUTO con FOR XML | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- FOR XML clause, AUTO mode
- ELEMENTS option
- FOR XML AUTO mode
- AUTO FOR XML mode
ms.assetid: 7140d656-1d42-4f01-a533-5251429f4450
caps.latest.revision: 31
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b665fc99fd92ecb2ff11a06a4d0a4f11186d96a1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="use-auto-mode-with-for-xml"></a>Usar el modo AUTO con FOR XML
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Tal como se describe en [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md), el modo AUTO devuelve los resultados de la consulta como elementos XML anidados. Esto no ofrece un gran control sobre la forma del XML generado a partir del resultado de una consulta. Las consultas en modo AUTO son útiles si desea generar jerarquías sencillas. Pero [Usar el modo EXPLICIT con FOR XML](../../relational-databases/xml/use-explicit-mode-with-for-xml.md) y [Usar el modo PATH con FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md) ofrecen mayor control y flexibilidad a la hora de decidir la forma del XML procedente del resultado de una consulta.  
  
 Cada tabla de la cláusula FROM, de la que al menos se presenta una columna en la cláusula SELECT, se representa como un elemento XML. Las columnas que se incluyen en la cláusula SELECT se asignan a atributos o subelementos, si se especifica la opción ELEMENTS en la cláusula FOR XML.  
  
 La jerarquía XML, anidamiento de los elementos, del XML resultante está basada en el orden de las tablas identificadas por las columnas especificadas en la cláusula SELECT. Por tanto, el orden en que se especifican los nombres de columna en la cláusula SELECT es importante. La primera, la tabla situada más a la izquierda que se identifica, constituye el elemento superior del documento XML resultante. La segunda tabla situada más a la izquierda, identificada por las columnas de la instrucción SELECT, constituye un subelemento del elemento superior, etc.  
  
 Si un nombre de columna que aparece en la cláusula SELECT procede de una tabla ya identificada por una columna especificada anteriormente en la cláusula SELECT, la columna se agrega como atributo del elemento ya creado, en lugar de abrir un nuevo nivel de jerarquía. Si se especifica la opción ELEMENTS, la columna se agrega como atributo.  
  
 Por ejemplo, ejecute esta consulta:  
  
```  
SELECT Cust.CustomerID,   
       OrderHeader.CustomerID,  
       OrderHeader.SalesOrderID,   
       OrderHeader.Status,  
       Cust.CustomerType  
FROM Sales.Customer Cust, Sales.SalesOrderHeader OrderHeader  
WHERE Cust.CustomerID = OrderHeader.CustomerID  
ORDER BY Cust.CustomerID  
FOR XML AUTO  
```  
  
 Éste es el resultado parcial:  
  
```  
<Cust CustomerID="1" CustomerType="S">  
  <OrderHeader CustomerID="1" SalesOrderID="43860" Status="5" />  
  <OrderHeader CustomerID="1" SalesOrderID="44501" Status="5" />  
  <OrderHeader CustomerID="1" SalesOrderID="45283" Status="5" />  
  <OrderHeader CustomerID="1" SalesOrderID="46042" Status="5" />  
</Cust>  
...  
```  
  
 Observe lo siguiente en la cláusula SELECT:  
  
-   CustomerID hace referencia a la tabla Cust. Por tanto, se crea un elemento <`Cust`> y se agrega CustomerID como su atributo.  
  
-   A continuación, tres columnas, OrderHeader.CustomerID, OrderHeader.SaleOrderID y OrderHeader.Status, hacen referencia a la tabla OrderHeader. Por tanto, se agrega un elemento <`OrderHeader`> como subelemento del elemento <`Cust`> y las tres columnas se agregan como atributos de <`OrderHeader`>.  
  
-   A continuación, la columna Cust.CustomerType hace referencia de nuevo a la tabla Cust, que ya se había identificado con la columna Cust.CustomerID. Por tanto, no se crea ningún elemento nuevo. En su lugar, se agrega el atributo CustomerType al elemento <`Cust`> que se había creado anteriormente.  
  
-   La consulta especifica alias para los nombres de tabla. Estos alias aparecen como nombres de los elementos correspondientes.  
  
-   ORDER BY es necesario para agrupar todos los elementos secundarios en un único elemento primario.  
  
 Esta consulta es similar a la anterior, pero la cláusula SELECT especifica columnas en la tabla OrderHeader antes de las columnas de la tabla Cust. Por tanto, se crea primero el elemento <`OrderHeader`> y después se le agrega el elemento secundario <`Cust`>.  
  
```  
select OrderHeader.CustomerID,  
       OrderHeader.SalesOrderID,   
       OrderHeader.Status,  
       Cust.CustomerID,   
       Cust.CustomerType  
from Sales.Customer Cust, Sales.SalesOrderHeader OrderHeader  
where Cust.CustomerID = OrderHeader.CustomerID  
for xml auto  
```  
  
 Éste es el resultado parcial:  
  
```  
<OrderHeader CustomerID="1" SalesOrderID="43860" Status="5">  
  <Cust CustomerID="1" CustomerType="S" />  
</OrderHeader>  
...  
```  
  
 Si se agrega la opción ELEMENTS a la cláusula FOR XML, se devuelve XML centrado en elementos.  
  
```  
SELECT Cust.CustomerID,   
       OrderHeader.CustomerID,  
       OrderHeader.SalesOrderID,   
       OrderHeader.Status,  
       Cust.CustomerType  
FROM Sales.Customer Cust, Sales.SalesOrderHeader OrderHeader  
WHERE Cust.CustomerID = OrderHeader.CustomerID  
ORDER BY Cust.CustomerID  
FOR XML AUTO, ELEMENTS  
```  
  
 Éste es el resultado parcial:  
  
```  
<Cust>  
  <CustomerID>1</CustomerID>  
  <CustomerType>S</CustomerType>  
  <OrderHeader>  
    <CustomerID>1</CustomerID>  
    <SalesOrderID>43860</SalesOrderID>  
    <Status>5</Status>  
  </OrderHeader>  
   ...  
</Cust>  
...  
```  
  
 En esta consulta, los valores CustomerID de una fila se comparan con los de la siguiente al crear elementos \<Cust>, porque CustomerID es la clave principal de la tabla. Si no se identifica CustomerID como clave principal de la tabla, todos los valores de columna (CustomerID, CustomerType en esta consulta) de una fila se comparan con los de la siguiente. Si los valores difieren, se agrega un nuevo elemento \<Cust> al XML.  
  
 Cuando se comparan estos valores de columna, si algunas de las columnas que se comparan son de tipo **text**, **ntext**, **image**o **xml**, FOR XML asume que los valores son diferentes y no los compara, incluso si son los mismos. Esto se debe a que no se admite la comparación de objetos grandes. Se agregan elementos al resultado para cada fila seleccionada. Tenga en cuenta que se comparan las columnas de **(n)varchar(max)** y **varbinary(max)** .  
  
 Si no se puede asociar una columna de la cláusula SELECT con ninguna de las tablas identificadas en la cláusula FROM, como en el caso de una columna de agregado o una columna calculada, se agrega la columna en el documento XML en el nivel de anidamiento más profundo cuando se encuentra en la lista. Si esa columna aparece como la primera de la cláusula SELECT, la columna se agrega al elemento superior.  
  
 Si se especifica el carácter comodín * (asterisco) en la cláusula SELECT, el anidamiento se determina del mismo modo que se ha explicado anteriormente, en función de las filas devueltas por el motor de consulta.  
  
## <a name="in-this-section"></a>En esta sección  
 Los temas siguientes proporcionan más información sobre el modo AUTO:  
  
-   [Usar la opción BINARY BASE64](../../relational-databases/xml/use-the-binary-base64-option.md)  
  
-   [Heurística del modo AUTO para dar forma al XML devuelto](../../relational-databases/xml/auto-mode-heuristics-in-shaping-returned-xml.md)  
  
-   [Ejemplos: Usar el modo AUTO](../../relational-databases/xml/examples-using-auto-mode.md)  
  
## <a name="see-also"></a>Ver también  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  
  
  
