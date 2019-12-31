---
title: Asignar tipos de datos XSD a tipos de datos de XPath (SQLXML)
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
ms.openlocfilehash: 6b956bf3a52b9ae14e59af770d279e8be8fec028
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/19/2019
ms.locfileid: "75257386"
---
# <a name="mapping-xsd-data-types-to-xpath-data-types-sqlxml-40"></a>Asignar tipos de datos de XSD a tipos de datos de XPath (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Cuando se ejecuta una consulta XPath en un esquema XSD y se especifica el tipo XSD en el atributo **xsd: Type** , XPath usa el tipo de datos especificado al procesar la consulta.  
  
 El tipo de datos XPath de un nodo se deriva del tipo de dato XSD del esquema, como se muestra en la tabla siguiente. (El nodo EmployeeID se usa a modo de ilustración.)  
  
|Tipo de datos XSD|Tipo de datos XDR|Tipo de datos de XPath<br /><br /> equivalente|SQL Server<br /><br /> conversión que se usa|  
|-------------------|-------------------|------------------------------------|--------------------------------------------|  
|**Base64Binary**<br /><br /> **HexBinary**|**Ninguno**<br /><br /> **bin. base64bin. hex**|**No aplicable**|Ninguno<br /><br /> EmployeeID|  
|**Boolean**|**booleano**|**booleano**|CONVERT (bit, IdEmpleado)|  
|**Decimal, integer, Float, byte, Short, int, Long, Float, Double, unsignedByte, unsignedShort, unsignedInt, unsignedLong**|**number, int, float,i1, i2, i4, i8,r4, r8ui1, ui2, ui4, ui8**|**números**|CONVERT(float(53), EmployeeID)|  
|**ID, idref, idrefsentity, Entities, Notation, NMTOKEN, NMTOKENS, DateTime, String, anyURI**|**ID, idref, idrefsentity, Entities, Enumeration, Notation, NMTOKEN, NMTOKENS, Char, dateTime, dateTime.tz, String, Uri, UUID**|**String@**|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|**decimal**|**fixed14.4**|**No aplicable (no hay ningún tipo de datos en XPath que sea equivalente al tipo de datos de XDR fijo fijo).**|CONVERT(money, EmployeeID)|  
|**Posteriormente**|**Posteriormente**|**String@**|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|**tiempo**|**tiempo**<br /><br /> **time.tz**|**String@**|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
  
