---
title: Formato XML en el servidor (SQLXML)
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- FOR XML clause, formatting
- server-side XML formatting
ms.assetid: ae9ea068-0857-4505-a3b2-f53d256b644c
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ec84fdfad468124f59cefde73486d5b19a5a4110
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/19/2019
ms.locfileid: "75255901"
---
# <a name="server-side-xml-formatting-sqlxml-40"></a>Aplicación de formato XML en el servidor (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
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
  
 Para obtener más información sobre la cláusula FOR XML, vea [generar XML mediante for XML](../../../relational-databases/xml/for-xml-sql-server.md).  
  
## <a name="see-also"></a>Véase también  
 [Arquitectura del formato XML del lado cliente y del lado servidor &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml/formatting/architecture-of-client-side-and-server-side-xml-formatting-sqlxml-4-0.md)   
 [Formato XML del lado cliente &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml/formatting/client-side-xml-formatting-sqlxml-4-0.md)   
 [SQL Server &#40;FOR XML&#41;](../../../relational-databases/xml/for-xml-sql-server.md)  
  
  
