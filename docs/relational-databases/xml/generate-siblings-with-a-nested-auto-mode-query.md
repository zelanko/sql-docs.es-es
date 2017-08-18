---
title: Generar elementos del mismo nivel con una consulta de modo AUTO anidada | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- queries [XML in SQL Server], nested AUTO mode
- nested AUTO mode query
ms.assetid: 748d9899-589d-4420-8048-1258e9e67c20
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 6d85a1b59656222cf07338d2eb98925e30a5c658
ms.contentlocale: es-es
ms.lasthandoff: 08/18/2017

---
# <a name="generate-siblings-with-a-nested-auto-mode-query"></a>Generar elementos del mismo nivel con una consulta de modo AUTO anidada
  En el siguiente ejemplo se muestra cómo generar elementos del mismo nivel utilizando una consulta en modo AUTO anidada. Solo hay otra forma de generar este XML, que es utilizar el modo EXPLICIT. Sin embargo, esto puede ser tedioso.  
  
## <a name="example"></a>Ejemplo  
 Esta consulta genera XML que proporciona información de pedidos de ventas. Incluye lo siguiente:  
  
-   Información de encabezado de pedidos de ventas, `SalesOrderID`, `SalesPersonID`y `OrderDate`. [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] almacena esta información en la tabla `SalesOrderHeader` .  
  
-   Información detallada de pedidos de ventas. Esto incluye uno o varios productos pedidos, el precio por unidad y la cantidad pedida. Esta información se almacena en la tabla `SalesOrderDetail` .  
  
-   Información del vendedor. Es el vendedor que tomó el pedido. En la tabla `SalesPerson` se proporciona el valor `SalesPersonID`. Para esta consulta, tiene que combinar esta tabla con la tabla `Employee` para buscar el nombre del vendedor.  
  
 Las dos consultas `SELECT` siguientes generan XML con una pequeña diferencia en la forma.  
  
 La primera consulta genera XML en el que <`SalesPerson`> y <`SalesOrderHeader`> aparecen como elementos secundarios iguales de <`SalesOrder`>:  
  
```  
SELECT   
      (SELECT top 2 SalesOrderID, SalesPersonID, CustomerID,  
         (select top 3 SalesOrderID, ProductID, OrderQty, UnitPrice  
           from Sales.SalesOrderDetail  
            WHERE  SalesOrderDetail.SalesOrderID =   
                   SalesOrderHeader.SalesOrderID  
            FOR XML AUTO, TYPE)  
        FROM  Sales.SalesOrderHeader  
        WHERE SalesOrderHeader.SalesOrderID = SalesOrder.SalesOrderID  
        for xml auto, type),  
        (SELECT *   
         FROM  (SELECT SalesPersonID, EmployeeID  
              FROM Sales.SalesPerson, HumanResources.Employee  
              WHERE SalesPerson.SalesPersonID = Employee.EmployeeID) As   
                     SalesPerson  
         WHERE  SalesPerson.SalesPersonID = SalesOrder.SalesPersonID  
       FOR XML AUTO, TYPE)  
FROM (SELECT SalesOrderHeader.SalesOrderID, SalesOrderHeader.SalesPersonID  
      FROM Sales.SalesOrderHeader, Sales.SalesPerson  
      WHERE SalesOrderHeader.SalesPersonID = SalesPerson.SalesPersonID  
     ) as SalesOrder  
ORDER BY SalesOrder.SalesOrderID  
FOR XML AUTO, TYPE  
```  
  
 En la consulta anterior, la instrucción `SELECT` más externa realiza las siguientes acciones:  
  
-   Consulta el conjunto de filas, `SalesOrder`, especificado en la cláusula `FROM`. El resultado es un XML con uno o varios elementos <`SalesOrder`>.  
  
-   Especifica el modo `AUTO` y la directiva `TYPE` . `AUTO` transforma el resultado de la consulta en XML y la directiva `TYPE` devuelve el resultado como tipo **xml** .  
  
-   Incluye dos instrucciones `SELECT` anidadas separadas por una coma. La primera instrucción `SELECT` anidada recupera información de pedidos de ventas, encabezado y detalles, y la segunda instrucción `SELECT` anidada recupera información del vendedor.  
  
    -   La instrucción `SELECT` que recupera `SalesOrderID`, `SalesPersonID`y `CustomerID` incluye otra instrucción `SELECT ... FOR XML` anidada (con el modo `AUTO` y la directiva `TYPE` ) que devuelve información de detalles de pedidos de venta.  
  
 La instrucción `SELECT` que recupera información del vendedor consulta un conjunto de filas, `SalesPerson`, creado en la cláusula `FROM` . Para que las consultas `FOR XML` funcionen, debe proporcionar un nombre para el conjunto de filas anónimo generado en la cláusula `FROM` . En este caso, el nombre proporcionado es `SalesPerson`.  
  
 Éste es el resultado parcial:  
  
```  
<SalesOrder>  
  <Sales.SalesOrderHeader SalesOrderID="43659" SalesPersonID="279" CustomerID="676">  
    <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="776" OrderQty="1" UnitPrice="2024.9940" />  
    <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="777" OrderQty="3" UnitPrice="2024.9940" />  
    <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="778" OrderQty="1" UnitPrice="2024.9940" />  
  </Sales.SalesOrderHeader>  
  <SalesPerson SalesPersonID="279" EmployeeID="279" />  
</SalesOrder>  
...  
```  
  
 La siguiente consulta genera la misma información de pedidos de ventas, pero en el XML resultante <`SalesPerson`> aparece como elemento de mismo nivel de <`SalesOrderDetail`>:  
  
```  
<SalesOrder>  
    <SalesOrderHeader ...>  
          <SalesOrderDetail .../>  
          <SalesOrderDetail .../>  
          ...  
          <SalesPerson .../>  
    </SalesOrderHeader>  
  
</SalesOrder>  
<SalesOrder>  
  ...  
</SalesOrder>  
```  
  
 Esta es la consulta:  
  
```  
SELECT SalesOrderID, SalesPersonID, CustomerID,  
             (select top 3 SalesOrderID, ProductID, OrderQty, UnitPrice  
              from Sales.SalesOrderDetail  
              WHERE SalesOrderDetail.SalesOrderID = SalesOrderHeader.SalesOrderID  
              FOR XML AUTO, TYPE),  
              (SELECT *   
               FROM  (SELECT SalesPersonID, EmployeeID  
                    FROM Sales.SalesPerson, HumanResources.Employee  
                    WHERE SalesPerson.SalesPersonID = Employee.EmployeeID) As SalesPerson  
               WHERE  SalesPerson.SalesPersonID = SalesOrderHeader.SalesPersonID  
         FOR XML AUTO, TYPE)  
FROM Sales.SalesOrderHeader  
WHERE SalesOrderID=43659 or SalesOrderID=43660  
FOR XML AUTO, TYPE  
```  
  
 El resultado es el siguiente:  
  
```  
<Sales.SalesOrderHeader SalesOrderID="43659" SalesPersonID="279" CustomerID="676">  
  <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="776" OrderQty="1" UnitPrice="2024.9940" />  
  <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="777" OrderQty="3" UnitPrice="2024.9940" />  
  <Sales.SalesOrderDetail SalesOrderID="43659" ProductID="778" OrderQty="1" UnitPrice="2024.9940" />  
  <SalesPerson SalesPersonID="279" EmployeeID="279" />  
</Sales.SalesOrderHeader>  
<Sales.SalesOrderHeader SalesOrderID="43660" SalesPersonID="279" CustomerID="117">  
  <Sales.SalesOrderDetail SalesOrderID="43660" ProductID="762" OrderQty="1" UnitPrice="419.4589" />  
  <Sales.SalesOrderDetail SalesOrderID="43660" ProductID="758" OrderQty="1" UnitPrice="874.7940" />  
  <SalesPerson SalesPersonID="279" EmployeeID="279" />  
</Sales.SalesOrderHeader>  
```  
  
 Puesto que la directiva `TYPE` devuelve un resultado de consulta de tipo **xml** , puede consultar el XML resultante utilizando varios métodos del tipo de datos **xml** . Para obtener más información, vea [Métodos de tipo de datos xml](../../t-sql/xml/xml-data-type-methods.md). En la siguiente consulta, tenga en cuenta lo siguiente:  
  
-   La consulta anterior se agrega a la cláusula `FROM` . El resultado de la consulta se devuelve como una tabla. Observe el alias `XmlCol` agregado.  
  
-   La cláusula `SELECT` especifica una consulta XQuery en el `XmlCol` devuelto en la cláusula `FROM` . Se usa el método **query()** del tipo de datos **xml** al especificar la consulta XQuery. Para obtener más información, vea [query&#40;&#41; &#40;método de tipo de datos xml&#41;](../../t-sql/xml/query-method-xml-data-type.md).  
  
    ```  
    SELECT XmlCol.query('<Root> { /* } </Root>')  
    FROM (  
    SELECT SalesOrderID, SalesPersonID, CustomerID,  
                 (select top 3 SalesOrderID, ProductID, OrderQty, UnitPrice  
                  from Sales.SalesOrderDetail  
                  WHERE SalesOrderDetail.SalesOrderID = SalesOrderHeader.SalesOrderID  
                  FOR XML AUTO, TYPE),  
                  (SELECT *   
                   FROM  (SELECT SalesPersonID, EmployeeID  
                        FROM Sales.SalesPerson, HumanResources.Employee  
                        WHERE SalesPerson.SalesPersonID = Employee.EmployeeID) As SalesPerson  
                   WHERE  SalesPerson.SalesPersonID = SalesOrderHeader.SalesPersonID  
             FOR XML AUTO, TYPE)  
    FROM Sales.SalesOrderHeader  
    WHERE SalesOrderID='43659' or SalesOrderID='43660'  
    FOR XML AUTO, TYPE ) as T(XmlCol)  
    ```  
  
## <a name="see-also"></a>Vea también  
 [Usar consultas FOR XML anidadas](../../relational-databases/xml/use-nested-for-xml-queries.md)  
  
  
