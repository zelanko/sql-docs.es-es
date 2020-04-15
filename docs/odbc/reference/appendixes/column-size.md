---
title: Tamaño de la columna ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], column size
- size of data types [ODBC]
- SQL data types [ODBC], column characteristics
- column size of data types [ODBC]
ms.assetid: 541b83ab-b16d-4714-bcb2-3c3daa9a963b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 07b6151c723cb5e05189791100338e9e343c28aa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306586"
---
# <a name="column-size"></a>Tamaño de columna
El tamaño de columna (o parámetro) de los tipos de datos numéricos se define como el número máximo de dígitos utilizados por el tipo de datos de la columna o parámetro, o la precisión de los datos. Para los tipos de caracteres, esta es la longitud en caracteres de los datos; para los tipos de datos binarios, el tamaño de columna se define como la longitud en bytes de los datos. Para la hora, la marca de tiempo y todos los tipos de datos de intervalo, este es el número de caracteres en la representación de caracteres de estos datos. El tamaño de columna definido para cada tipo de datos SQL conciso se muestra en la tabla siguiente.  
  
|Identificador de tipo SQL|Tamaño de la columna|  
|-------------------------|-----------------|  
|Todos los tipos de caracteres[a],[b]|El tamaño de columna definido o máximo en caracteres de la columna o parámetro (como se incluye en el campo descriptor de SQL_DESC_LENGTH). Por ejemplo, el tamaño de columna de una columna de caracteres de un solo byte definida como CHAR(10) es 10.|  
|SQL_DECIMAL SQL_NUMERIC|El número definido de dígitos. Por ejemplo, la precisión de una columna definida como NUMERIC(10,3) es 10.|  
|SQL_BIT[c]|1|  
|SQL_TINYINT[c]|3|  
|SQL_SMALLINT[c]|5|  
|SQL_INTEGER[c]|10|  
|SQL_BIGINT[c]|19 (si está firmado) o 20 (si no está firmado)|  
|SQL_REAL[c]|7|  
|SQL_FLOAT[c]|15|  
|SQL_DOUBLE[c]|15|  
|Todos los tipos binarios[a],[b]|La longitud definida o máxima en bytes de la columna o parámetro. Por ejemplo, la longitud de una columna definida como BINARY(10) es 10.|  
|SQL_TYPE_DATE[c]|10 (el número de caracteres en el formato *aaaa-mm-dd).*|  
|SQL_TYPE_TIME[c]|8 (el número de caracteres en el formato *hh-mm-ss),* o 9 + *s* (el número de caracteres en el formato *hh:mm:ss*[.fff...], donde *s* es la precisión de segundos).|  
|SQL_TYPE_TIMESTAMP|16 (el número de caracteres en el formato *aaaa-mm-dd hh:mm)*<br /><br /> 19 (el número de caracteres en el formato *aaaa-mm-dd* *hh:mm:ss)*<br /><br /> or<br /><br /> 20 + *s* (el número de caracteres en el formato *aaaa-mm-dd hh:mm:ss*[.fff...], donde *s* es la precisión de los segundos).|  
|SQL_INTERVAL_SECOND|Donde *p* es la precisión inicial del intervalo y *s* es la precisión de segundos, *p* (si *s*s) o *p*+*s*+1 (si *s*>0). [d]|  
|SQL_INTERVAL_DAY_TO_SECOND|Donde *p* es la precisión inicial del intervalo y *s* es la precisión de los segundos, 9+*p* (si *s*s) o 10+*p*+*s* (si *s*>0). [d]|  
|SQL_INTERVAL_HOUR_TO_SECOND|Donde *p* es la precisión inicial del intervalo y *s* es la precisión de los segundos, 6+*p* (si *s*s) o 7+*p*+*s* (si *s*>0). [d]|  
|SQL_INTERVAL_MINUTE_TO_SECOND|Donde *p* es la precisión inicial del intervalo y *s* es la precisión de los segundos, 3+*p* (si *s*s) o 4+*p*+*s* (si *s*>0). [d]|  
|SQL_INTERVAL_YEAR SQL_INTERVAL_MONTH SQL_INTERVAL_DAY SQL_INTERVAL_HOUR SQL_INTERVAL_MINUTE|*p*, donde *p* es la precisión inicial del intervalo. [d]|  
|SQL_INTERVAL_YEAR_TO_MONTH SQL_INTERVAL_DAY_TO_HOUR|3+*p*, donde *p* es la precisión de interlineado del intervalo. [d]|  
|SQL_INTERVAL_DAY_TO_MINUTE|6+*p*, donde *p* es la precisión de interlineado del intervalo. [d]|  
|SQL_INTERVAL_HOUR_TO_MINUTE|3+*p*, donde *p* es la precisión de interlineado del intervalo. [d]|  
|SQL_GUID|36 (el número de caracteres en el formato *aaaaaaaa-bbbb-cccc-dddd-eeeeeeeeeeee)*|  
  
 [a] Para una aplicación ODBC 1.0 que llama a **SQLSetParam** en un controlador ODBC 2.0 y para una \*aplicación ODBC 2.0 que llama a **SQLBindParameter** en un controlador ODBC 1.0, cuando *StrLen_or_IndPtr* es SQL_DATA_AT_EXEC para un tipo de SQL_LONGVARCHAR o SQL_LONGVARBINARY, *ColumnSize* debe establecerse en la longitud total de los datos que se enviarán, no en la precisión definida en esta tabla.  
  
 [b] Si el controlador no puede determinar la longitud de columna o parámetro para un tipo de variable, devuelve SQL_NO_TOTAL.  
  
 [c] El *ColumnSize* argumento de **SQLBindParameter** se omite para este tipo de datos.  
  
 [d] Para obtener reglas generales sobre la longitud de columna en tipos de datos de intervalo, consulte [Longitud](../../../odbc/reference/appendixes/interval-data-type-length.md)del tipo de datos de intervalo , anteriormente en este apéndice.  
  
 Los valores devueltos para el tamaño de columna (o parámetro) no corresponden a los valores de ningún campo descriptor. Los valores pueden provenir del campo SQL_DESC_PRECISION o SQL_DESC_LENGTH, dependiendo del tipo de datos, como se muestra en la tabla siguiente.  
  
|Tipo SQL|Campo descriptor correspondiente a<br /><br /> tamaño de columna o parámetro|  
|--------------|--------------------------------------------------------------------|  
|Todos los tipos de caracteres y binarios|LENGTH|  
|Todos los tipos numéricos|PRECISION|  
|Todos los tipos de fecha y hora e intervalo|LENGTH|  
|SQL_BIT|LENGTH|
