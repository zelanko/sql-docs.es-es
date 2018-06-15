---
title: 'Ejemplo: Especificar las directivas ID e IDREFS | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- IDREFS directive
- ID directive
ms.assetid: 99b9f0d8-ecbb-4225-859f-881066c09785
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5483235964a1b10decad823313e3657809a7d34a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33013822"
---
# <a name="example-specifying-the-id-and-idrefs-directives"></a>Ejemplo: Especificar las directivas ID e IDREFS
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  El atributo de un elemento se puede especificar como un atributo de tipo **ID** y el atributo **IDREFS** puede usarse para hacer referencia a él. De esta forma se habilitan vínculos dentro de los documentos; esto es similar a las relaciones entre la clave principal y la clave externa en las bases de datos relacionales.  
  
 Este ejemplo ilustra cómo se pueden usar las directivas **ID** e **IDREFS** para crear atributos de tipos **ID** e **IDREFS** . Dado que los identificadores no pueden contener valores enteros, los valores ID de este ejemplo se convierten. Dicho de otro modo, se realiza una conversión de tipos. Para los valores ID se utilizan prefijos.  
  
 Suponga que desea crear XML como se indica a continuación:  
  
```  
<Customer CustomerID="C1" SalesOrderIDList=" O11 O22 O33..." >  
    <SalesOrder SalesOrderID="O11" OrderDate="..." />  
    <SalesOrder SalesOrderID="O22" OrderDate="..." />  
    <SalesOrder SalesOrderID="O33" OrderDate="..." />  
    ...  
</Customer>  
```  
  
 El atributo `SalesOrderIDList` del elemento < `Customer` > es un atributo con varios valores que hace referencia al atributo `SalesOrderID` del elemento < `SalesOrder` >. Para establecer este vínculo, el atributo `SalesOrderID` debe declararse de tipo `ID` y el atributo `SalesOrderIDList` del elemento < `Customer`> debe declararse de tipo `IDREFS`. Dado que un cliente puede solicitar varios pedidos, se utiliza el tipo `IDREFS`.  
  
 Los elementos del tipo **IDREFS** también tienen más de un valor. Por lo tanto, se tiene que utilizar una cláusula SELECT independiente, que volverá a utilizar la misma información de columna de clave, etiqueta y elemento primario. Luego, `ORDER BY` tiene que asegurarse de que la secuencia de filas que componen los valores de **IDREFS** aparezca agrupada bajo el elemento primario.  
  
 Esta es la consulta que genera el XML deseado. La consulta utiliza las directivas `ID` e `IDREFS` para sobrescribir los tipos en los nombres de columna (`SalesOrder!2!SalesOrderID!ID`, `Customer!1!SalesOrderIDList!IDREFS`).  
  
```  
USE AdventureWorks2012;  
GO  
SELECT  1 as Tag,  
        0 as Parent,  
        C.CustomerID       [Customer!1!CustomerID],  
        NULL               [Customer!1!SalesOrderIDList!IDREFS],  
        NULL               [SalesOrder!2!SalesOrderID!ID],  
        NULL               [SalesOrder!2!OrderDate]  
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
    ON  C.CustomerID = SOH.CustomerIDORDER BY [Customer!1!CustomerID] ,  
         [SalesOrder!2!SalesOrderID!ID],  
         [Customer!1!SalesOrderIDList!IDREFS]  
FOR XML EXPLICIT;  
```  
  
## <a name="see-also"></a>Ver también  
 [Usar el modo EXPLICIT con FOR XML](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
  
  
