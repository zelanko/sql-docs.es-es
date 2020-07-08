---
title: 'Ejemplo: Especificación de las directivas ID e IDREFS | Microsoft Docs'
description: Obtenga información sobre cómo la especificación de las directivas ID e IDREFS en una consulta SQL puede habilitar vínculos dentro de documentos.
ms.custom: fresh2019may
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- IDREFS directive
- ID directive
ms.assetid: 99b9f0d8-ecbb-4225-859f-881066c09785
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d38a541f1c323199e02a86f0c0e23cd5b5620659
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85632329"
---
# <a name="example-specifying-the-id-and-idrefs-directives"></a>Ejemplo: Especificación de las directivas ID e IDREFS

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

El atributo de un elemento se puede especificar como un atributo de tipo **ID** y el atributo **IDREFS** puede usarse para hacer referencia a él. De esta forma se habilitan vínculos dentro de los documentos; esto es similar a las relaciones entre la clave principal y la clave externa en las bases de datos relacionales.  
  
 Este ejemplo ilustra cómo se pueden usar las directivas **ID** e **IDREFS** para crear atributos de tipos **ID** e **IDREFS** . Dado que los identificadores no pueden contener valores enteros, los valores ID de este ejemplo se convierten. Dicho de otro modo, se realiza una conversión de tipos. Para los valores ID se utilizan prefijos.  
  
 Suponga que desea crear XML como se indica a continuación:  
  
```xml
<Customer CustomerID="C1" SalesOrderIDList=" O11 O22 O33..." >
    <SalesOrder SalesOrderID="O11" OrderDate="..." />  
    <SalesOrder SalesOrderID="O22" OrderDate="..." />  
    <SalesOrder SalesOrderID="O33" OrderDate="..." />  
    ...  
</Customer>  
```  
  
El atributo `SalesOrderIDList` del elemento `<Customer>` es un atributo con varios valores que hace referencia al atributo `SalesOrderID` del elemento `<SalesOrder>`. Para establecer este vínculo, el atributo `SalesOrderID` debe declararse de tipo `ID` y el atributo `SalesOrderIDList` del elemento `<Customer>` debe declararse de tipo `IDREFS`. Dado que un cliente puede solicitar varios pedidos, se utiliza el tipo `IDREFS` .
  
 Los elementos del tipo **IDREFS** también tienen más de un valor. Por lo tanto, se tiene que utilizar una cláusula SELECT independiente, que volverá a utilizar la misma información de columna de clave, etiqueta y elemento primario. Luego, `ORDER BY` tiene que asegurarse de que la secuencia de filas que componen los valores de **IDREFS** aparezca agrupada bajo el elemento primario.  
  
 Esta es la consulta que genera el XML deseado. La consulta utiliza las directivas `ID` e `IDREFS` para sobrescribir los tipos en los nombres de columna (`SalesOrder!2!SalesOrderID!ID`, `Customer!1!SalesOrderIDList!IDREFS`).  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT  1 as Tag,  
        0 as Parent,  
        C.CustomerID   [Customer!1!CustomerID],  
        NULL           [Customer!1!SalesOrderIDList!IDREFS],
        NULL           [SalesOrder!2!SalesOrderID!ID],  
        NULL           [SalesOrder!2!OrderDate]  
FROM   Sales.Customer C   

UNION ALL   
SELECT  1 as Tag,  
        0 as Parent,  
        C.CustomerID,  
        'O-'+CAST(SalesOrderID as varchar(10)),   
        NULL,  
        NULL  
FROM   Sales.Customer AS C  
INNER JOIN Sales.SalesOrderHeader AS SOH  
    ON  C.CustomerID = SOH.CustomerID  

UNION ALL  
SELECT 2 as Tag,  
       1 as Parent,  
        C.CustomerID,  
        NULL,  
        'O-'+CAST(SalesOrderID as varchar(10)),  
        OrderDate  
FROM   Sales.Customer AS C  
INNER JOIN Sales.SalesOrderHeader AS SOH  
    ON  C.CustomerID = SOH.CustomerID
ORDER BY [Customer!1!CustomerID] ,
         [SalesOrder!2!SalesOrderID!ID],  
         [Customer!1!SalesOrderIDList!IDREFS]  
FOR XML EXPLICIT;  
```  
  
## <a name="see-also"></a>Consulte también  
 [Usar el modo EXPLICIT con FOR XML](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
  
  
