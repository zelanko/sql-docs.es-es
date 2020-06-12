---
title: Asignar tipos de datos XSD a tipos de datos de XPath (SQLXML)
description: Obtenga información acerca de cómo asignar tipos de datos XSD a tipos de datos de XPath al realizar una consulta XPath en SQLXML 4,0.
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- mapping data types [SQLXML]
- data types [SQLXML], converting
- annotated XSD schemas, mapping data types
- XPath queries [SQLXML], mapping data types
- converting data types [SQLXML]
- data types [SQLXML], mapping data types
- XPath data types [SQLXML]
- XSD schemas [SQLXML], mapping data types
ms.assetid: ced1a95e-18d4-4a5a-8da8-dbb6d58bbd45
author: MightyPen
ms.author: genemi
ms.reviewer: ''
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1dd2800d89016223e172e11ebde2cc3f8332e7d4
ms.sourcegitcommit: 9921501952147b9ce3e85a1712495d5b3eb13e5b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/29/2020
ms.locfileid: "84215708"
---
# <a name="mapping-xsd-data-types-to-xpath-data-types-sqlxml-40"></a>Asignar tipos de datos de XSD a tipos de datos de XPath (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Cuando se ejecuta una consulta XPath en un esquema XSD y se especifica el tipo XSD en el atributo **xsd: Type** , XPath usa el tipo de datos especificado al procesar la consulta.  
  
 El tipo de datos XPath de un nodo se deriva del tipo de dato XSD del esquema, como se muestra en la tabla siguiente. (El nodo EmployeeID se usa a modo de ilustración.)  
  
|Tipo de datos XSD|Tipo de datos XDR|Tipo de datos de XPath<br /><br /> equivalente|SQL Server<br /><br /> conversión que se usa|  
|-------------------|-------------------|------------------------------------|--------------------------------------------|  
|**Base64Binary**<br /><br /> **HexBinary**|**None**<br /><br /> **bin. base64bin. hex**|**No aplicable**|None<br /><br /> EmployeeID|  
|**Boolean**|**boolean**|**boolean**|CONVERT (bit, IdEmpleado)|  
|**Decimal, integer, Float, byte, Short, int, Long, Float, Double, unsignedByte, unsignedShort, unsignedInt, unsignedLong**|**number, int, float,i1, i2, i4, i8,r4, r8ui1, ui2, ui4, ui8**|**número**|CONVERT(float(53), EmployeeID)|  
|**ID, idref, idrefsentity, Entities, Notation, NMTOKEN, NMTOKENS, DateTime, String, anyURI**|**ID, idref, idrefsentity, Entities, Enumeration, Notation, NMTOKEN, NMTOKENS, Char, dateTime, dateTime.tz, String, Uri, UUID**|**string**|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|**decimal**|**fixed14.4**|**No aplicable (no hay ningún tipo de datos en XPath que sea equivalente al tipo de datos de XDR fijo fijo).**|CONVERT(money, EmployeeID)|  
|**date**|**date**|**string**|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|**time**|**time**<br /><br /> **time.tz**|**string**|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
  
