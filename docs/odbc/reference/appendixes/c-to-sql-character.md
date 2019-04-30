---
title: 'C a SQL: Carácter | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- character data type [ODBC]
- data conversions from C to SQL types [ODBC], character
- converting data from c to SQL types [ODBC], character
ms.assetid: be66188a-ebdb-4c9e-af72-c379886766fa
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0158da62ed360e926cdb5382b89b1491c0723550
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63201626"
---
# <a name="c-to-sql-character"></a>C a SQL: Carácter
Los identificadores para el carácter de tipo de datos ODBC C son:  
  
 SQL_C_CHAR  
  
 SQL_C_WCHAR  
  
 La siguiente tabla muestra los tipos de datos a la que se pueden convertir los datos de caracteres de C de ODBC SQL. Para obtener una explicación de las columnas y los términos de la tabla, vea [convertir datos de C a tipos de datos SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
> [!NOTE]  
>  Cuando los datos de caracteres de C se convierte en datos Unicode SQL, la longitud de los datos Unicode debe ser un número par.  
  
|Identificador de tipo SQL|Prueba|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Longitud de bytes de datos < = longitud de la columna.<br /><br /> Longitud de bytes de datos > longitud de la columna.|n/d<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Longitud de los datos de carácter < = longitud de la columna.<br /><br /> Longitud de datos de caracteres > longitud de la columna.|n/d<br /><br /> 22001|  
|SQL_DECIMAL<br /><br /> SQL_NUMERIC<br /><br /> SQL_TINYINT<br /><br /> SQL_SMALLINT<br /><br /> SQL_INTEGER SQL_BIGINT|Puede convertidas sin truncamiento de datos<br /><br /> Convierten datos con el truncamiento de dígitos fraccionarios [e]<br /><br /> Conversión de datos daría lugar a pérdida de dígitos de entero (en contraposición a fraccionarios) [e]<br /><br /> Valor de datos no es un *literales numéricos*|n/d<br /><br /> 22001<br /><br /> 22001<br /><br /> 22018|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|Datos están dentro del intervalo del tipo de datos a la que se va a convertir el número<br /><br /> Datos están fuera del intervalo del tipo de datos a la que se va a convertir el número<br /><br /> Valor de datos no es un *literales numéricos*|n/d<br /><br /> 22003<br /><br /> 22018|  
|SQL_BIT|Datos están 0 o 1<br /><br /> Datos están mayores que 0, inferior a 2 y no es igual a 1<br /><br /> Datos están menor que 0 o mayor que o igual a 2<br /><br /> Datos no están un *literales numéricos*|n/d<br /><br /> 22001<br /><br /> 22003<br /><br /> 22018|  
|SQL_BINARY<br /><br /> SQL_VARBINARY<br /><br /> SQL_LONGVARBINARY|(Longitud de bytes de datos) / 2 < = longitud de bytes de la columna<br /><br /> (Longitud de bytes de datos) / 2 > longitud de bytes de la columna<br /><br /> Valor de datos no es un valor hexadecimal|n/d<br /><br /> 22001<br /><br /> 22018|  
|SQL_TYPE_DATE|Valor de datos es válido *literal de fecha ODBC*<br /><br /> Valor de datos es válido *literal de marca de tiempo de ODBC*; parte de hora es cero<br /><br /> Valor de datos es válido *literal de marca de tiempo de ODBC*; parte de hora es distinto de cero [a]<br /><br /> Valor de datos no es válido *literal de fecha ODBC* o *literal de marca de tiempo de ODBC*|n/d<br /><br /> n/d<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIME|Valor de datos es válido *literal de hora ODBC*<br /><br /> Valor de datos es válido *literal de marca de tiempo de ODBC*; fraccionarios parte de segundos es cero [b]<br /><br /> Valor de datos es válido *literal de marca de tiempo de ODBC*; fraccionarios parte de segundos es distinto de cero [b]<br /><br /> Valor de datos no es válido *literal de hora ODBC* o *literal de marca de tiempo de ODBC*|n/d<br /><br /> n/d<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIMESTAMP|Valor de datos es válido *literal de marca de tiempo de ODBC*; fraccionarios parte de los segundos no se ha truncado<br /><br /> Valor de datos es válido *literal de marca de tiempo de ODBC*; fraccionarios truncado parte de los segundos<br /><br /> Valor de datos es válido *literal de fecha ODBC*[c]<br /><br /> Valor de datos es válido *literal de hora ODBC*[d]<br /><br /> Valor de datos no es válido *literal de fecha ODBC*, *literal de hora ODBC*, o *literal de marca de tiempo de ODBC*|n/d<br /><br /> 22008<br /><br /> n/d<br /><br /> n/d<br /><br /> 22018|  
|Todos los tipos de intervalo SQL|Valor de datos es válido *el valor de intervalo*; se produce ningún truncamiento<br /><br /> Valor de datos es válido *el valor de intervalo*; se trunca el valor en uno de los campos<br /><br /> El valor de datos no es un literal de intervalo válido|n/d<br /><br /> 22015<br /><br /> 22018|  
  
 [a] se trunca la parte de hora de la marca de tiempo.  
  
 [b] la parte de fecha de la marca de tiempo se omite.  
  
 [c] la parte de hora de la marca de tiempo se establece en cero.  
  
 [d] la parte de fecha de la marca de tiempo se establece en la fecha actual.  
  
 [e] el origen de datos/controlador eficazmente espera hasta que se ha recibido la cadena completa (incluso si los datos de caracteres se enviaron por partes mediante llamadas a **SQLPutData**) antes de intentar realizar la conversión.  
  
 Cuando los datos de carácter C convertido a numérico, fecha, hora o marca de tiempo de datos de SQL, iniciales y finales de los espacios en blanco se omiten.  
  
 Cuando los datos de caracteres de C se convierte en datos binarios de SQL, cada dos bytes de datos de caracteres se convierten en un solo byte (8 bits) de datos binarios. Cada dos bytes de datos de caracteres se representan un número en formato hexadecimal. Por ejemplo, "01" se convierte en un binario 00000001 y "FF" se convierte en un binario 11111111.  
  
 El controlador siempre convierte los pares de dígitos hexadecimales en bytes individuales y omite los bytes de terminación null. Por este motivo, si la longitud de la cadena de caracteres es impar, no se convierte el último byte de la cadena (excepto el byte de una terminación null, si existe).  
  
> [!NOTE]  
>  Los desarrolladores de aplicaciones se desaconseja el enlace de datos de carácter C a un tipo binario de datos SQL. Esta conversión suele ser ineficaz y lento.
