---
title: Ejemplos de conversión de datos de C a SQL ( C to SQL Data Conversion Examples) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], examples
- data conversions from C to SQL types [ODBC], examples
ms.assetid: 9f390afc-d8b8-4286-b559-98b3b8781f3d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0e21654f183946675c63cee10a3c08754e1508f5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81291995"
---
# <a name="c-to-sql-data-conversion-examples"></a>Ejemplos de conversión de datos de C en SQL
Los siguientes ejemplos ilustran cómo el controlador convierte los datos de C en datos SQL:  
  
|Identificador de tipo C|Valor de datos C|Tipo SQL<br /><br /> identificador|Columna<br /><br /> length|SQL data<br /><br /> value|SQLSTATE|  
|-----------------------|------------------|-----------------------------|-----------------------|------------------------|--------------|  
|SQL_C_CHAR|abcdef-0[a]|SQL_CHAR|6|abcdef|N/D|  
|SQL_C_CHAR|abcdef-0[a]|SQL_CHAR|5|Abcde|22001|  
|SQL_C_CHAR|1234.56-0[a]|SQL_DECIMAL|8[b]|1234.56|N/D|  
|SQL_C_CHAR|1234.56-0[a]|SQL_DECIMAL|7[b]|1234.5|22001|  
|SQL_C_CHAR|1234.56-0[a]|SQL_DECIMAL|4|----|22003|  
|SQL_C_FLOAT|1234.56|SQL_FLOAT|N/D|1234.56|N/D|  
|SQL_C_FLOAT|1234.56|SQL_INTEGER|N/D|1234|22001|  
|SQL_C_FLOAT|1234.56|SQL_TINYINT|N/D|----|22003|  
|SQL_C_TYPE_DATE|1992,12,31[c]|SQL_CHAR|10|1992-12-31|N/D|  
|SQL_C_TYPE_DATE|1992,12,31[c]|SQL_CHAR|9|----|22003|  
|SQL_C_TYPE_DATE|1992,12,31[c]|SQL_TIMESTAMP|N/D|1992-12-31 00:00:00.0|N/D|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31, 23,45,55, 120000000[d]|SQL_CHAR|22|1992-12-31 23:45:55.12|N/D|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31, 23,45,55, 120000000[d]|SQL_CHAR|21|1992-12-31 23:45:55.1|22001|  
|SQL_C_TYPE_TIMESTAMP|1992,12,31, 23,45,55, 120000000[d]|SQL_CHAR|18|----|22003|  
  
 [a] "-0" representa un byte de terminación nula. El byte de terminación nula solo es necesario si se SQL_NTS la longitud de los datos.  
  
 [b] Además de bytes para números, se requiere un byte para un signo y otro byte para el punto decimal.  
  
 [c] Los números de esta lista son los números almacenados en los campos de la estructura SQL_DATE_STRUCT.  
  
 [d] Los números de esta lista son los números almacenados en los campos de la estructura SQL_TIMESTAMP_STRUCT.
