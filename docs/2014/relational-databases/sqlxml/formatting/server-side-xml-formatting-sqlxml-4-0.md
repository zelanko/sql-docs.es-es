---
title: Formato XML en el servidor (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- FOR XML clause, formatting
- server-side XML formatting
ms.assetid: ae9ea068-0857-4505-a3b2-f53d256b644c
author: rothja
ms.author: jroth
ms.openlocfilehash: 707c1389f1a1a97d904617ebb54cbf5c5495a9d1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065700"
---
# <a name="server-side-xml-formatting-sqlxml-40"></a>Aplicación de formato XML en el servidor (SQLXML 4.0)
  En este tema se proporciona información sobre cómo aplicar formato a los documentos XML en el servidor desde los conjuntos de filas generados por consultas ejecutadas en una base de datos de Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 En [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], puede almacenar y recuperar los documentos XML en y de las tablas de base de datos. Para recuperar un documento XML, utilice la extensión de consulta FOR XML en una consulta SELECT.  
  
 Por ejemplo, suponga que una aplicación cliente ejecuta un comando en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que consta de la siguiente [!INCLUDE[tsql](../../../includes/tsql-md.md)] consulta:  
  
```  
SELECT FirstName, LastName  
FROM   Person.Contact  
FOR XML AUTO  
```  
  
 El servidor ejecuta la consulta en dos pasos. Primero, el servidor ejecuta esta instrucción SELECT:  
  
```  
SELECT FirstName, LastName  
FROM   Person.Contact  
```  
  
 A continuación, el servidor aplica la transformación FOR XML al conjunto de filas generado. A continuación, el XML resultante se envía al cliente como un conjunto de filas de una columna. En esta documentación, este proceso se conoce como aplicación de formato XML en el servidor.  
  
 En el servidor, puede especificar los modos siguientes con una cláusula FOR XML:  
  
-   RAW  
  
-   AUTO  
  
-   EXPLICIT  
  
 Para obtener más información sobre la cláusula FOR XML, vea [generar XML mediante for XML](../../xml/for-xml-sql-server.md).  
  
## <a name="see-also"></a>Consulte también  
 [Arquitectura del formato XML del lado cliente y del lado servidor &#40;SQLXML 4,0&#41;](architecture-of-client-side-and-server-side-xml-formatting-sqlxml-4-0.md)   
 [Formato XML del lado cliente &#40;SQLXML 4,0&#41;](client-side-xml-formatting-sqlxml-4-0.md)   
 [FOR XML &#40;SQL Server&#41;](../../xml/for-xml-sql-server.md)  
  
  
