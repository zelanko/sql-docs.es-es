---
title: Tipos de datos de Microsoft Access | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b99fd70e0119aa01d384066aaa2f3b91eed152b4
ms.sourcegitcommit: 480961f14405dc0b096aa8009855dc5a2964f177
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/22/2019
ms.locfileid: "54420180"
---
# <a name="microsoft-access-data-types"></a>Tipos de datos de Microsoft Access
En la tabla siguiente se muestra los tipos de datos de Microsoft Access, tipos de datos utilizados para crear tablas y los tipos de datos SQL de ODBC.  
  
|Tipo de datos de Microsoft Access|Tipo de datos (CREATETABLE)|Tipo de datos SQL de ODBC|  
|--------------------------------|-------------------------------|------------------------|  
|BIGBINARY [1]|LONGBINARY|SQL_LONGVARBINARY|  
|BINARY|BINARY|SQL_BINARY|  
|BIT|BIT|SQL_BIT|  
|CONTADOR|CONTADOR|SQL_INTEGER|  
|Moneda|Moneda|SQL_NUMERIC|  
|FECHA Y HORA|DATETIME|SQL_TIMESTAMP|  
|GUID|GUID|SQL_GUID|  
|BINARIO LARGO|LONGBINARY|SQL_LONGVARBINARY|  
|TEXTO LARGO|LONGTEXT|SQL_LONGVARCHAR[2] SQL_WLONGVARCHAR[3]|  
|MEMORANDO|LONGTEXT|SQL_LONGVARCHAR[2] SQL_WLONGVARCHAR[3]|  
|NÚMERO (tamaño del campo = SOLTERO)|ÚNICO|SQL_REAL|  
|NÚMERO (tamaño del campo = doble)|DOUBLE|SQL_DOUBLE|  
|NÚMERO (tamaño del campo = BYTE)|BYTE SIN SIGNO|SQL_TINYINT|  
|NÚMERO (tamaño del campo = entero)|CORTO|SQL_SMALLINT|  
|NÚMERO (tamaño del campo = entero largo)|LONG|SQL_INTEGER|  
|NUMERIC|NUMERIC|SQL_NUMERIC|  
|OLE|LONGBINARY|SQL_LONGVARBINARY|  
|TEXT|VARCHAR|SQL_VARCHAR[1] SQL_WVARCHAR[2]|  
|VARBINARY|VARBINARY|SQL_VARBINARY|  
  
 [1] aplicaciones de acceso 4.0. Longitud máxima de 4.000 bytes. Comportamiento es similar al LONGBINARY.  
  
 [2] solo las aplicaciones ANSI.  
  
 [3] Unicode y acceso 4.0 sólo aplicaciones.  
  
> [!NOTE]  
>  **SQLGetTypeInfo** devuelve tipos de datos ODBC. Si se asigna más de un tipo de Microsoft Access en el mismo tipo de datos SQL de ODBC no devolverá todos los tipos de datos de Microsoft Access. Todas las conversiones en el apéndice D de la *referencia del programador de ODBC* son compatibles con los tipos de datos SQL de la tabla anterior.  
  
 La siguiente tabla muestra las limitaciones en los tipos de datos de Microsoft Access.  
  
|Tipo de datos|Descripción|  
|---------------|-----------------|  
|BINARY, VARBINARY y VARCHAR|Creación de una columna BINARY, VARBINARY o VARCHAR de cero o sin especificar longitud devuelve realmente una columna de bytes de 510.|  
|BYTE|Aunque un campo de número de acceso de Microsoft con un tamaño igual a BYTE es sin signo, un número negativo puede insertarse en el campo cuando se utiliza el controlador de Microsoft Access.|  
|VARCHAR, LONGVARCHAR y CHAR|Un literal de cadena de caracteres puede contener cualquier carácter ANSI (de 1 a 255 decimal). Usar dos consecutivos comillas (") para representar una comilla simple (').<br /><br /> Procedimientos deben utilizarse para pasar datos de caracteres al usar cualquier carácter especial en una columna de tipo de datos de caracteres.|  
|DATE|Los valores de fecha deben ser delimitados según el formato de fecha canónica de ODBC o delimitados por el delimitador de fecha y hora ("#"). En caso contrario, Microsoft Access tratará el valor como una expresión aritmética y no generará una advertencia o error.<br /><br /> Por ejemplo, la fecha de "5 de marzo de 1996" se debe representar como {d. ' 05-03-1996 "} o #03/05/1996 #; en caso contrario, si sólo se envía 03/05/1993, Microsoft Access se evaluará esto como 3 dividido entre 5 dividido por 1996. Este valor se redondea al entero de 0, y dado que el día cero se asigna a 1899-12-31, esta es la fecha que se usa.<br /><br /> Un carácter de barra vertical (&#124;) no se puede usar en un valor de fecha, aun cuando de retroceso entre comillas.|  
|GUID|Tipo de datos limitada a 4.0 de Microsoft Access.|  
|NUMERIC|Tipo de datos limitada a 4.0 de Microsoft Access.|  
  
 Para conocer más limitaciones en los tipos de datos pueden encontrarse en [limitaciones del tipo de datos](../../odbc/microsoft/data-type-limitations.md).
