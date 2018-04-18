---
title: Tipos de datos de Microsoft Access | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Access driver
- Jet-based ODBC drivers [ODBC], Access driver
- desktop database drivers [ODBC], Access driver
- Access driver [ODBC], data types
- access data types [ODBC]
- data types [ODBC], Access driver
ms.assetid: b537348a-bea0-4bd6-84a4-52a75292957f
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Active
ms.openlocfilehash: 8faac619846998c1be7bc0577761b94bf6dc27ba
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="microsoft-access-data-types"></a>Tipos de datos de Microsoft Access
La tabla siguiente muestran los tipos de datos de Microsoft Access, tipos de datos utilizados para crear tablas y tipos de datos SQL de ODBC.  
  
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
|TEXTO LARGO|LONGTEXT|SQL_WLONGVARCHAR SQL_LONGVARCHAR [2] [3]|  
|MEMORANDO|LONGTEXT|SQL_WLONGVARCHAR SQL_LONGVARCHAR [2] [3]|  
|NÚMERO (tamaño del campo = SOLTERO)|ÚNICO|SQL_REAL|  
|NÚMERO (tamaño del campo = doble)|DOUBLE|SQL_DOUBLE|  
|NÚMERO (tamaño del campo = BYTE)|BYTE SIN SIGNO|SQL_TINYINT|  
|NÚMERO (tamaño del campo = entero)|CORTO|SQL_SMALLINT|  
|NÚMERO (tamaño del campo = entero largo)|LONG|SQL_INTEGER|  
|NUMERIC|NUMERIC|SQL_NUMERIC|  
|OLE|LONGBINARY|SQL_LONGVARBINARY|  
|TEXT|VARCHAR|SQL_WVARCHAR SQL_VARCHAR [1] [2]|  
ARBINARY|VARBINARY|SQL_VARBINARY|  
  
 [1] aplicaciones de acceso 4.0. Longitud máxima de 4000 bytes. Comportamiento es similar al LONGBINARY.  
  
 [2] aplicaciones de ANSI.  
  
 [3] aplicaciones de Unicode y acceso 4.0 solo.  
  
> [!NOTE]  
>  **SQLGetTypeInfo** devuelve tipos de datos ODBC. No devolverá todos los tipos de datos de Microsoft Access si hay asignado más de un tipo de Microsoft Access en el mismo tipo de datos SQL de ODBC. Todas las conversiones en el apéndice D de la *referencia del programador de ODBC* son compatibles con los tipos de datos SQL que aparecen en la tabla anterior.  
  
 La siguiente tabla muestra las limitaciones en los tipos de datos de Microsoft Access.  
  
|Tipo de datos|Description|  
|---------------|-----------------|  
|BINARY, VARBINARY y VARCHAR|Creación de una columna BINARY, VARBINARY o VARCHAR de cero o sin especificar longitud realmente devuelve una columna 510 bytes.|  
|BYTE|Aunque un campo de número de acceso de Microsoft con un tamaño en bytes del campo es sin signo, un número negativo se puede insertar en el campo cuando se utiliza el controlador de Microsoft Access.|  
|VARCHAR, CHAR y LONGVARCHAR|Un literal de cadena de caracteres puede contener cualquier carácter ANSI (1-255 decimal). Utilice dos consecutivos comillas (") para representar una comilla simple (').<br /><br /> Los procedimientos se deben utilizar para pasar datos de caracteres cuando se utiliza ningún carácter especial en una columna de tipo de datos de caracteres.|  
|DATE|Los valores de fecha deben ser delimitados según el formato de fecha canónica de ODBC o delimitados por el delimitador de fecha y hora ("#"). En caso contrario, Microsoft Access tratará el valor como una expresión aritmética y no generará una advertencia o error.<br /><br /> Por ejemplo, la fecha de "5 de marzo de 1996" se deben representar como {d. ' 1996-03-05'} o #03/05/1996 #; en caso contrario, si sólo se envía 03/05/1993, Microsoft Access evaluará esta como 3 dividido entre 5 dividido por 1996. Este valor se redondea al entero 0 y, puesto que el día cero se asigna a 1899-12-31, se trata de la fecha utilizada.<br /><br /> Un carácter de barra vertical (&#124;) no se puede usar en un valor de fecha, incluso si en la parte posterior entre comillas.|  
|GUID|Tipo de datos limitado a 4.0 de Microsoft Access.|  
|NUMERIC|Tipo de datos limitado a 4.0 de Microsoft Access.|  
  
 Para conocer más limitaciones en los tipos de datos pueden encontrarse en [limitaciones del tipo de datos](../../odbc/microsoft/data-type-limitations.md).
