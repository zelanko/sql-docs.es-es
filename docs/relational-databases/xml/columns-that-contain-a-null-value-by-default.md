---
title: Columnas que incluyen un valor NULL de forma predeterminada | Microsoft Docs
ms.custom: fresh2019may
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- columns [XML in SQL Server], null default value
ms.assetid: 9381c07f-6887-4a62-9730-32661f9aa87c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f7672d59b2355c0733a5e26da6217fbabf729c6a
ms.sourcegitcommit: 68583d986ff5539fed73eacb7b2586a71c37b1fa
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/04/2020
ms.locfileid: "80664705"
---
# <a name="columns-that-contain-a-null-value-by-default"></a>Columnas que incluyen un valor NULL de forma predeterminada

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

De forma predeterminada, un valor NULL en una columna se asigna a la ausencia del atributo, nodo u elemento. Este comportamiento predeterminado puede invalidarse mediante el uso de la frase de palabras clave ELEMENTS XSINIL. Esta frase solicita un XML centrado en elementos. Esto significa que los valores null se indican explícitamente en los resultados devueltos. Estos elementos no tendrán ningún valor.

La frase ELEMENTS XSINIL se muestra en el siguiente ejemplo Transact-SQL SELECT.

```sql
SELECT EmployeeID as "@EmpID",   
       FirstName  as "EmpName/First",   
       MiddleName as "EmpName/Middle",   
       LastName   as "EmpName/Last"  
FROM   HumanResources.Employee E, Person.Contact C  
WHERE  E.EmployeeID = C.ContactID  
  AND  E.EmployeeID=1
FOR XML PATH, ELEMENTS XSINIL;
```  
  
 A continuación se muestra el resultado. Tenga en cuenta que si no se especifica XSINIL, el elemento <`Middle`> estará ausente.  
  
```xml
<row xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
    <Middle xsi:nil="true" />  
    <Last>Achong</Last>  
  </EmpName>  
</row>  
```  
  
## <a name="see-also"></a>Consulte también  
 [Usar el modo PATH con FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
