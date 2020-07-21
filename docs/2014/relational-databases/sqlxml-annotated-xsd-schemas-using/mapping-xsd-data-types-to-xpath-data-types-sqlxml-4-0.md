---
title: Asignar tipos de datos XSD a tipos de datos de XPath (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
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
author: rothja
ms.author: jroth
ms.openlocfilehash: a4a3bd0b100dd935b5cea0d9ee4565633a9cb80e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85003200"
---
# <a name="mapping-xsd-data-types-to-xpath-data-types-sqlxml-40"></a>Asignar tipos de datos de XSD a tipos de datos de XPath (SQLXML 4.0)
  Cuando se ejecuta una consulta XPath con un esquema XSD y se especifica el tipo XSD en el atributo `xsd:type`, XPath usa el tipo de datos especificado al procesar la consulta.  
  
 El tipo de datos XPath de un nodo se deriva del tipo de dato XSD del esquema, como se muestra en la tabla siguiente. (El nodo EmployeeID se usa a modo de ilustración.)  
  
|Tipo de datos XSD|Tipo de datos XDR|Tipo de datos de XPath<br /><br /> equivalente|SQL Server<br /><br /> conversión que se usa|  
|-------------------|-------------------|------------------------------------|--------------------------------------------|  
|`Base64Binary`<br /><br /> `HexBinary`|`None`<br /><br /> `bin.base64bin.hex`|`Not applicable`|None<br /><br /> EmployeeID|  
|`Boolean`|`boolean`|`boolean`|CONVERT (bit, IdEmpleado)|  
|`Decimal, integer, float, byte, short, int, long, float, double, unsignedByte, unsignedShort, unsignedInt, unsignedLong`|`number, int, float,i1, i2, i4, i8,r4, r8ui1, ui2, ui4, ui8`|`number`|CONVERT(float(53), EmployeeID)|  
|`id, idref, idrefsentity, entities, notation, nmtoken, nmtokens, DateTime, string, AnyURI`|`id, idref, idrefsentity, entities, enumeration, notation, nmtoken, nmtokens, char, dateTime, dateTime.tz, string, uri, uuid`|`string`|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|`decimal`|`fixed14.4`|`Not applicable (There is no data type in XPath that is equivalent to the fixed14.4 XDR data type.)`|CONVERT(money, EmployeeID)|  
|`date`|`date`|`string`|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|`time`|`time`<br /><br /> `time.tz`|`string`|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
  
