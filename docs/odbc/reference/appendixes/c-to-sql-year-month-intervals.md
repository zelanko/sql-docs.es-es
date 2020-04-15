---
title: 'C a SQL: Intervalos año-mes Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], year-month intervals
- intervals [ODBC], converting
- year-month intervals [ODBC]
- data conversions from C to SQL types [ODBC], year-month intervals
ms.assetid: a0eb7b55-9db0-4375-9210-bddec4593880
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2ec7bfda0015883c8470dd453c7ae5de9bfd6cec
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306616"
---
# <a name="c-to-sql-year-month-intervals"></a>C a SQL: Intervalos de mes y año
Los identificadores de los tipos de datos ODBC C de intervalo de año-mes son:  
  
 SQL_C_INTERVAL_MONTH SQL_C_INTERVAL_YEAR SQL_C_INTERVAL_YEAR_TO_MONTH  
  
 En la tabla siguiente se muestran los tipos de datos SQL ODBC a los que se pueden convertir los datos de intervalo C de un año-mes. Para obtener una explicación de las columnas y los términos de la tabla, vea [Convertir datos de C a tipos](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)de datos SQL .  
  
|Identificador de tipo SQL|Prueba|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR[a]<br /><br /> SQL_VARCHAR[a]<br /><br /> SQL_LONGVARCHAR[a]|Longitud de bytes de columna >- Longitud de byte de caracteres<br /><br /> Longitud de bytes de columna < Longitud de byte de caracteres[a]<br /><br /> El valor de los datos no es un literal de intervalo válido|N/D<br /><br /> 22001<br /><br /> 22015|  
|SQL_WCHAR[a]<br /><br /> SQL_WVARCHAR[a]<br /><br /> SQL_WLONGVARCHAR[a]|Longitud de caracteres de columna >- Longitud de caracteres de datos<br /><br /> Longitud de caracteres de columna < Longitud de caracteres de datos[a]<br /><br /> El valor de los datos no es un literal de intervalo válido|N/D<br /><br /> 22001<br /><br /> 22015|  
|SQL_TINYINT[b]<br /><br /> SQL_SMALLINT[b]<br /><br /> SQL_INTEGER[b]<br /><br /> SQL_BIGINT[b]<br /><br /> SQL_NUMERIC[b]<br /><br /> SQL_DECIMAL[b]|La conversión de un intervalo de un solo campo no dio lugar al truncamiento de dígitos enteros<br /><br /> La conversión dio lugar al truncamiento de dígitos enteros|N/D<br /><br /> 22003|  
|SQL_INTERVAL_MONTH<br /><br /> SQL_INTERVAL_YEAR<br /><br /> SQL_INTERVAL_YEAR_TO_MONTH|El valor de datos se convirtió sin truncamiento de ningún campo<br /><br /> Uno o más campos de valor de datos se truncaron durante la conversión|N/D<br /><br /> 22015|  
  
 [a] Todos los tipos de datos de intervalo C se pueden convertir en un tipo de datos de carácter.  
  
 [b] Si el campo de tipo de la estructura de intervalo es tal que el intervalo es un solo campo (SQL_YEAR o SQL_MONTH), el tipo de intervalo C se puede convertir a cualquier número exacto (SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_DECIMAL o SQL_NUMERIC).  
  
 La conversión predeterminada de un tipo de intervalo C es al tipo SQL de intervalo de año-mes correspondiente.  
  
 El controlador omite el valor de longitud/indicador al convertir datos del tipo de datos de intervalo C y asume que el tamaño del búfer de datos es el tamaño del tipo de datos de intervalo C. El valor de longitud/indicador se pasa en el argumento *StrLen_or_Ind* en **SQLPutData** y en el búfer especificado con el argumento *StrLen_or_IndPtr* en **SQLBindParameter**. El búfer de datos se especifica con el *argumento DataPtr* en **SQLPutData** y el argumento *ParameterValuePtr* en **SQLBindParameter**.
