---
title: Tipos de datos de Microsoft Access ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Access driver
- Jet-based ODBC drivers [ODBC], Access driver
- desktop database drivers [ODBC], Access driver
- Access driver [ODBC], data types
- access data types [ODBC]
- data types [ODBC], Access driver
ms.assetid: b537348a-bea0-4bd6-84a4-52a75292957f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 024fb65b6fdc81ae0a8e007d1cee150c6a35b91c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307734"
---
# <a name="microsoft-access-data-types"></a>Tipos de datos de Microsoft Access
En la tabla siguiente se muestran los tipos de datos de Microsoft Access, los tipos de datos utilizados para crear tablas y los tipos de datos SQL ODBC.  
  
|Tipo de datos de Microsoft Access|Tipo de datos (CREATETABLE)|Tipo de datos ODBC SQL|  
|--------------------------------|-------------------------------|------------------------|  
|BIGBINARY[1]|LONGBINARY|SQL_LONGVARBINARY|  
|BINARY|BINARY|SQL_BINARY|  
|BIT|BIT|SQL_BIT|  
|Contador|Contador|SQL_INTEGER|  
|Moneda|Moneda|SQL_NUMERIC|  
|FECHA/HORA|DATETIME|SQL_TIMESTAMP|  
|GUID|GUID|SQL_GUID|  
|LONG BINARIO|LONGBINARY|SQL_LONGVARBINARY|  
|TEXTO LARGO|LONGTEXT|SQL_LONGVARCHAR[2] SQL_WLONGVARCHAR[3]|  
|memorándum|LONGTEXT|SQL_LONGVARCHAR[2] SQL_WLONGVARCHAR[3]|  
|Numero (Tamaño de campo SINGLE)|soltero|SQL_REAL|  
|Numero (Tamaño de campo DOBLE)|DOUBLE|SQL_DOUBLE|  
|Numero (Tamaño de campo BYTE)|UNSIGNED BYTE|SQL_TINYINT|  
|NUMERO (Tamaño de campo INTEGER)|SHORT|SQL_SMALLINT|  
|Numero (FieldSize - LONG INTEGER)|LONG|SQL_INTEGER|  
|NUMERIC|NUMERIC|SQL_NUMERIC|  
|OLE|LONGBINARY|SQL_LONGVARBINARY|  
|TEXT|VARCHAR|SQL_VARCHAR[1] SQL_WVARCHAR[2]|  
|VARBINARY|VARBINARY|SQL_VARBINARY|  
  
 [1] Solo acceso a aplicaciones 4.0. Longitud máxima de 4000 bytes. Comportamiento similar a LONGBINARY.  
  
 [2] Sólo aplicaciones ANSI.  
  
 [3] Solo aplicaciones Unicode y Access 4.0.  
  
> [!NOTE]  
>  **SQLGetTypeInfo** devuelve tipos de datos ODBC. No devolverá todos los tipos de datos de Microsoft Access si se asigna más de un tipo de Microsoft Access al mismo tipo de datos SQL ODBC. Todas las conversiones en el Apéndice D de la *Referencia del programador ODBC* son compatibles con los tipos de datos SQL enumerados en la tabla anterior.  
  
 En la tabla siguiente se muestran las limitaciones en los tipos de datos de Microsoft Access.  
  
|Tipo de datos|Descripción|  
|---------------|-----------------|  
|BINARY, VARBINARY y VARCHAR|La creación de una columna BINARY, VARBINARY o VARCHAR de longitud cero o no especificada devuelve realmente una columna de 510 bytes.|  
|BYTE|Aunque un campo NUMBER de Microsoft Access con un FieldSize igual a BYTE no está firmado, se puede insertar un número negativo en el campo cuando se usa el controlador de Microsoft Access.|  
|CHAR, LONGVARCHAR y VARCHAR|Un literal de cadena de caracteres puede contener cualquier carácter ANSI (1-255 decimal). Utilice dos comillas simples consecutivas ('') para representar una comilla simple (').<br /><br /> Los procedimientos se deben usar para pasar datos de caracteres cuando se utiliza cualquier carácter especial en una columna de tipo de datos de carácter.|  
|DATE|Los valores de fecha deben estar delimitados según el formato de fecha canónica ODBC o delimitados por el delimitador datetime ("."). De lo contrario, Microsoft Access tratará el valor como una expresión aritmética y no generará una advertencia o error.<br /><br /> Por ejemplo, la fecha "5 de marzo de 1996" debe representarse como "d'1996-03-05" o #03/05/1996;; de lo contrario, si sólo se envía 03/05/1993, Microsoft Access lo evaluará como 3 dividido por 5 dividido por 1996. Este valor redondea hasta el entero 0, y puesto que el día cero se asigna a 1899-12-31, esta es la fecha utilizada.<br /><br /> Un carácter de tubería (&#124;) no se puede utilizar en un valor de fecha, incluso si se incluye entre comillas inversas.|  
|GUID|Tipo de datos limitado a Microsoft Access 4.0.|  
|NUMERIC|Tipo de datos limitado a Microsoft Access 4.0.|  
  
 Puede encontrar más limitaciones en los tipos de datos en [Limitaciones](../../odbc/microsoft/data-type-limitations.md)de tipos de datos .
