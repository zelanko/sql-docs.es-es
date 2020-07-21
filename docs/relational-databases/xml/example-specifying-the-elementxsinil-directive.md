---
title: 'Ejemplo: Especificación de la directiva ELEMENTXSINIL | Microsoft Docs'
description: Obtenga información sobre cómo especificar la directiva ELEMENTXSINIL en SQL para generar elementos XML para valores NULL donde el atributo xsi:nil es true.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- ELEMENTXSINIL directive
ms.assetid: bbcb6f9e-a51b-4775-9795-947c9d6d758f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 64e44b8f84f2ff4b908556b31b6088a6a2c77c55
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85632507"
---
# <a name="example-specifying-the-elementxsinil-directive"></a>Ejemplo: Especificación de la directiva ELEMENTXSINIL
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Cuando se especifica la directiva ELEMENT para recuperar XML centrado en elementos, si la columna tiene algún valor NULL, el modo EXPLICIT no genera el elemento correspondiente. Opcionalmente, se puede especificar la directiva ELEMENTXSINIL para solicitar al elemento que se genera valores NULL donde el atributo **xsi:nil** esté establecido con el valor TRUE.  
  
 La consulta siguiente genera XML que incluye una dirección del empleado. Para las columnas `AddressLine2` y `City` , los nombres de columna especifican la directiva `ELEMENTXSINIL` . Así, se genera el elemento para los valores NULL en las columnas `AddressLine2` y `City` del conjunto de filas.  
  
```sql
USE AdventureWorks2012;  
GO  
SELECT 1    as Tag,  
       NULL as Parent,  
       E.BusinessEntityID  as [Employee!1!EmpID],  
       BEA.AddressID as [Employee!1!AddressID],  
       NULL        as [Address!2!AddressID],  
       NULL        as [Address!2!AddressLine1!ELEMENT],  
       NULL        as [Address!2!AddressLine2!ELEMENTXSINIL],  
       NULL        as [Address!2!City!ELEMENTXSINIL]  
FROM   HumanResources.Employee AS E  
INNER JOIN Person.BusinessEntityAddress AS BEA  
    ON E.BusinessEntityID = BEA.BusinessEntityID  
  
UNION ALL  
SELECT 2 as Tag,  
       1 as Parent,  
       E.BusinessEntityID,  
       BEA.AddressID,  
       A.AddressID,  
       AddressLine1,   
       AddressLine2,  
       City   
FROM   HumanResources.Employee AS E  
INNER JOIN Person.BusinessEntityAddress AS BEA  
    ON E.BusinessEntityID = BEA.BusinessEntityID  
INNER JOIN Person.Address AS A  
    ON BEA.AddressID = A.AddressID  
ORDER BY [Employee!1!EmpID],[Address!2!AddressID]  
FOR XML EXPLICIT;  
```  
  
 Éste es el resultado parcial:  

```xml
<Employee xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
          EmpID="1"
          AddressID="249">
  <Address AddressID="249">
    <AddressLine1>4350 Minute Dr.</AddressLine1>
    <AddressLine2 xsi:nil="true" />
    <City>Minneapolis</City>
  </Address>
</Employee>
...
```
  
## <a name="see-also"></a>Consulte también  
 [Usar el modo EXPLICIT con FOR XML](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
  
  
