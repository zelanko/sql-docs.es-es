---
title: Columnas que incluyen un valor NULL de forma predeterminada | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- columns [XML in SQL Server], null default value
ms.assetid: 9381c07f-6887-4a62-9730-32661f9aa87c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5d2b56355b21043f37e8d5991a453cc038064dce
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51674984"
---
# <a name="columns-that-contain-a-null-value-by-default"></a>Columnas que incluyen un valor NULL de forma predeterminada
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  De forma predeterminada, un valor NULL en una columna se asigna a la ausencia del atributo, nodo u elemento. Este comportamiento predeterminado se puede sobrescribir solicitando XML centrado en elementos mediante la directiva ELEMENTS y especificando XSINIL a fin de solicitar la adición de elementos para valores NULL, tal y como se muestra en la consulta siguiente:  
  
```  
SELECT EmployeeID as "@EmpID",   
       FirstName  as "EmpName/First",   
       MiddleName as "EmpName/Middle",   
       LastName   as "EmpName/Last"  
FROM   HumanResources.Employee E, Person.Contact C  
WHERE  E.EmployeeID = C.ContactID  
AND    E.EmployeeID=1  
FOR XML PATH, ELEMENTS XSINIL  
```  
  
 A continuación se muestra el resultado. Tenga en cuenta que si no se especifica XSINIL, el elemento <`Middle`> estará ausente.  
  
```  
<row xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" EmpID="1">  
  <EmpName>  
    <First>Gustavo</First>  
    <Middle xsi:nil="true" />  
    <Last>Achong</Last>  
  </EmpName>  
</row>  
```  
  
## <a name="see-also"></a>Ver también  
 [Usar el modo PATH con FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
