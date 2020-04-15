---
title: 'C a SQL: Carácter ? Microsoft Docs'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: acde0d2a79492607185d56d3082797c79a100fa2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292036"
---
# <a name="c-to-sql-character"></a>C a SQL: Carácter
Los identificadores para el tipo de datos ODBC C de caracteres son:  
  
 SQL_C_CHAR  
  
 SQL_C_WCHAR  
  
 En la tabla siguiente se muestran los tipos de datos SQL ODBC a los que se pueden convertir los datos de caracteres de C. Para obtener una explicación de las columnas y los términos de la tabla, vea [Convertir datos de C a tipos](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)de datos SQL .  
  
> [!NOTE]  
>  Cuando los datos de caracteres C se convierten en datos SQL Unicode, la longitud de los datos Unicode debe ser un número par.  
  
|Identificador de tipo SQL|Prueba|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|La longitud de los bytes de los <de datos: Longitud de columna.<br /><br /> Longitud de bytes de datos > Longitud de columna.|N/D<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|La longitud de los caracteres de los <de datos: Longitud de columna.<br /><br /> Longitud de caracteres de los datos > Longitud de columna.|N/D<br /><br /> 22001|  
|SQL_DECIMAL<br /><br /> SQL_NUMERIC<br /><br /> SQL_TINYINT<br /><br /> SQL_SMALLINT<br /><br /> SQL_INTEGER SQL_BIGINT|Datos convertidos sin truncamiento<br /><br /> Datos convertidos con truncamiento de dígitos fraccionarios[e]<br /><br /> La conversión de datos daría lugar a la pérdida de dígitos enteros (a diferencia de los fraccionarios)[e]<br /><br /> El valor de los datos no es un *literal numérico*|N/D<br /><br /> 22001<br /><br /> 22001<br /><br /> 22018|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|Los datos están dentro del rango del tipo de datos al que se está convirtiendo el número<br /><br /> Los datos están fuera del rango del tipo de datos al que se está convirtiendo el número<br /><br /> El valor de los datos no es un *literal numérico*|N/D<br /><br /> 22003<br /><br /> 22018|  
|SQL_BIT|Los datos son 0 o 1<br /><br /> Los datos son mayores que 0, menos que 2, y no iguales a 1<br /><br /> Los datos son menores o mayores o iguales que 2<br /><br /> Los datos no son un *literal numérico*|N/D<br /><br /> 22001<br /><br /> 22003<br /><br /> 22018|  
|SQL_BINARY<br /><br /> SQL_VARBINARY<br /><br /> SQL_LONGVARBINARY|(Longitud de bytes de los datos) / 2 <de la longitud de los bytes de columna<br /><br /> (Longitud de bytes de datos) / 2 > longitud de byte de columna<br /><br /> El valor de los datos no es un valor hexadecimal|N/D<br /><br /> 22001<br /><br /> 22018|  
|SQL_TYPE_DATE|El valor de datos es un valor *ODBC-fecha-literal* válido<br /><br /> El valor de datos es un literal *de marca de tiempo ODBC*válido; porción de tiempo es cero<br /><br /> El valor de datos es un literal *de marca de tiempo ODBC*válido; porción de tiempo es distinto de cero[a]<br /><br /> El valor de datos no es un *ODBC-date-literal* o *ODBC-timestamp-literal*|N/D<br /><br /> N/D<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIME|El valor de datos es un *literal de tiempo ODBC* válido<br /><br /> El valor de datos es un literal *de marca de tiempo ODBC*válido; fracción de segundos es cero[b]<br /><br /> El valor de datos es un literal *de marca de tiempo ODBC*válido; parte de fracciones de segundo es distinta de cero[b]<br /><br /> El valor de datos no es un *literal de tiempo ODBC* válido o un literal de marca de tiempo *ODBC*|N/D<br /><br /> N/D<br /><br /> 22008<br /><br /> 22018|  
|SQL_TYPE_TIMESTAMP|El valor de datos es un literal *de marca de tiempo ODBC*válido; porción de fracciones de segundo no truncada<br /><br /> El valor de datos es un literal *de marca de tiempo ODBC*válido; porción de fracciones de segundo truncada<br /><br /> El valor de datos es un *odbc-fecha-literal*válido [c]<br /><br /> El valor de datos es un *literal de tiempo ODBC*válido [d]<br /><br /> El valor de datos no es un *odbc-date-literal*válido, *ODBC-time-literal*u *ODBC-timestamp-literal*|N/D<br /><br /> 22008<br /><br /> N/D<br /><br /> N/D<br /><br /> 22018|  
|Todos los tipos de intervalosqlm|El valor de datos es un valor de *intervalo*válido; no se produce ningún truncamiento<br /><br /> El valor de datos es un valor de *intervalo*válido; el valor en uno de los campos se trunca<br /><br /> El valor de datos no es un literal de intervalo válido|N/D<br /><br /> 22015<br /><br /> 22018|  
  
 [a] La parte de tiempo de la marca de tiempo se trunca.  
  
 [b] Se omite la parte de fecha de la marca de tiempo.  
  
 [c] La parte de tiempo de la marca de tiempo se establece en cero.  
  
 [d] La parte de fecha de la marca de tiempo se establece en la fecha actual.  
  
 [e] El controlador/origen de datos espera eficazmente hasta que se haya recibido toda la cadena (incluso si los datos de caracteres se envían en partes mediante llamadas a **SQLPutData)** antes de intentar realizar la conversión.  
  
 Cuando los datos de caracteres C se convierten en datos SQL numéricos, de fecha, de hora o de marca de tiempo, se omiten los espacios en blanco iniciales y finales.  
  
 Cuando los datos de caracteres C se convierten en datos SQL binarios, cada dos bytes de datos de caracteres se convierten en un solo byte (8 bits) de datos binarios. Cada dos bytes de datos de caracteres representan un número en formato hexadecimal. Por ejemplo, "01" se convierte en un binario 00000001 y "FF" se convierte en un binario 11111111.  
  
 El controlador siempre convierte pares de dígitos hexadecimales en bytes individuales e ignora el byte de terminación nula. Por este problema, si la longitud de la cadena de caracteres es impar, el último byte de la cadena (excluyendo el byte de terminación nula, si existe) no se convierte.  
  
> [!NOTE]  
>  Se desaconseja a los desarrolladores de aplicaciones enlazar datos de caracteres C a un tipo de datos SQL binario. Esta conversión suele ser ineficiente y lenta.
