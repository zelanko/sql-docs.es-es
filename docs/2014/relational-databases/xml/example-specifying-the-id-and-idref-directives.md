---
title: 'Ejemplo: Especificación de las directivas ID e IDREF | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- IDREF directive
- ID directive
ms.assetid: 7ff1ea73-71ca-4786-bd42-564f1b5de2d9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f985745f450b402781685ded5c0a655e3f4e497c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62704832"
---
# <a name="example-specifying-the-id-and-idref-directives"></a>Ejemplo: Especificación de las directivas ID e IDREF
  Este ejemplo es casi idéntico al ejemplo [Especificar la directiva ELEMENTXSINIL](example-specifying-the-elementxsinil-directive.md) . La única diferencia consiste en que la consulta especifica las directivas **ID** e **IDREF** . Estas directivas sobrescriben los tipos del atributo **SalesPersonID** en los elementos <`OrderHeader`> y <`OrderDetail`>. De este modo, se forman vínculos dentro de los documentos. Para ver los tipos sobrescritos, se necesita el esquema. Por lo tanto, la consulta especifica la opción **XMLDATA** en la cláusula FOR XML para recuperar el esquema.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT  1 as Tag,  
        0 as Parent,  
        SalesOrderID  as [OrderHeader!1!SalesOrderID!id],  
        OrderDate     as [OrderHeader!1!OrderDate],  
        CustomerID    as [OrderHeader!1!CustomerID],  
        NULL          as [SalesPerson!2!SalesPersonID],  
        NULL          as [OrderDetail!3!SalesOrderID!idref],  
        NULL          as [OrderDetail!3!LineTotal],  
        NULL          as [OrderDetail!3!ProductID],  
        NULL          as [OrderDetail!3!OrderQty]  
FROM   Sales.SalesOrderHeader  
WHERE  SalesOrderID=43659 or SalesOrderID=43661  
UNION ALL   
SELECT 2 as Tag,  
       1 as Parent,  
        SalesOrderID,   
        NULL,  
        NULL,  
        SalesPersonID,    
        NULL,           
        NULL,           
        NULL,  
        NULL           
FROM   Sales.SalesOrderHeader  
WHERE  SalesOrderID=43659 or SalesOrderID=43661  
UNION ALL  
SELECT 3 as Tag,  
       1 as Parent,  
        SOD.SalesOrderID,  
        NULL,  
        NULL,  
        SalesPersonID,  
        SOH.SalesOrderID,  
        LineTotal,  
        ProductID,  
        OrderQty     
FROM    Sales.SalesOrderHeader SOH,Sales.SalesOrderDetail SOD  
WHERE   SOH.SalesOrderID = SOD.SalesOrderID  
AND     (SOH.SalesOrderID=43659 or SOH.SalesOrderID=43661)  
ORDER BY [OrderHeader!1!SalesOrderID!id], [SalesPerson!2!SalesPersonID],  
         [OrderDetail!3!SalesOrderID!idref],[OrderDetail!3!LineTotal]  
FOR XML EXPLICIT, XMLDATA  
```  
  
 El resultado parcial es el siguiente. En el esquema, observe que las directivas **ID** e **IDREF** han sobrescrito los tipos de datos del atributo **SalesOrderID** en los elementos <`OrderHeader`> y <`OrderDetail`>. Si quita estas directivas, el esquema devuelve los tipos originales de estos atributos.  
  
```  
<Schema name="Schema1" xmlns="urn:schemas-microsoft-com:xml-data" xmlns:dt="urn:schemas-microsoft-com:datatypes">  
  <ElementType name="OrderHeader" content="mixed" model="open">  
    <AttributeType name="SalesOrderID" dt:type="id" />  
    <AttributeType name="OrderDate" dt:type="dateTime" />  
    <AttributeType name="CustomerID" dt:type="i4" />  
    <attribute type="SalesOrderID" />  
    <attribute type="OrderDate" />  
    <attribute type="CustomerID" />  
  </ElementType>  
  <ElementType name="SalesPerson" content="mixed" model="open">  
    <AttributeType name="SalesPersonID" dt:type="i4" />  
    <attribute type="SalesPersonID" />  
  </ElementType>  
  <ElementType name="OrderDetail" content="mixed" model="open">  
    <AttributeType name="SalesOrderID" dt:type="idref" />  
    <AttributeType name="LineTotal" dt:type="number" />  
    <AttributeType name="ProductID" dt:type="i4" />  
    <AttributeType name="OrderQty" dt:type="i2" />  
    <attribute type="SalesOrderID" />  
    <attribute type="LineTotal" />  
    <attribute type="ProductID" />  
    <attribute type="OrderQty" />  
  </ElementType>  
</Schema>  
<OrderHeader xmlns="x-schema:#Schema1" SalesOrderID="43659" OrderDate="2001-07-01T00:00:00" CustomerID="676">  
  <SalesPerson SalesPersonID="279" />  
  <OrderDetail SalesOrderID="43659" LineTotal="10.373000" ProductID="712" OrderQty="2" />  
  ...  
</OrderHeader>  
...  
```  
  
## <a name="see-also"></a>Vea también  
 [Usar el modo EXPLICIT con FOR XML](use-explicit-mode-with-for-xml.md)  
  
  
