---
title: 'C a SQL: Intervalos de mes del año | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3db8d61bacefa8588db4c0081c6be591d7ffdacf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019286"
---
# <a name="c-to-sql-year-month-intervals"></a>C a SQL: Intervalos de mes y año
Los identificadores de los tipos de datos ODBC C de año y mes intervalo son:  
  
 SQL_C_INTERVAL_MONTH SQL_C_INTERVAL_YEAR SQL_C_INTERVAL_YEAR_TO_MONTH  
  
 En la tabla siguiente se muestra el SQL de ODBC para el mes de año intervalo C datos se pueden convertir los tipos de datos. Para obtener una explicación de las columnas y los términos de la tabla, vea [convertir datos de C a tipos de datos SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificador de tipo SQL|Prueba|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR[a]<br /><br /> SQL_VARCHAR[a]<br /><br /> SQL_LONGVARCHAR[a]|Longitud de bytes de la columna > = longitud de bytes de caracteres<br /><br /> Longitud de bytes de la columna < [a] longitud de bytes de caracteres<br /><br /> Valor de datos no es un intervalo válido de literal|N/D<br /><br /> 22001<br /><br /> 22015|  
|SQL_WCHAR [a]<br /><br /> SQL_WVARCHAR [a]<br /><br /> SQL_WLONGVARCHAR[a]|Longitud de caracteres de la columna > = longitud de caracteres de datos<br /><br /> Longitud de caracteres de la columna < caracteres de longitud de datos [a]<br /><br /> Valor de datos no es un intervalo válido de literal|N/D<br /><br /> 22001<br /><br /> 22015|  
|SQL_TINYINT[b]<br /><br /> SQL_SMALLINT[b]<br /><br /> SQL_INTEGER[b]<br /><br /> SQL_BIGINT[b]<br /><br /> SQL_NUMERIC[b]<br /><br /> SQL_DECIMAL [b]|Conversión de un intervalo de campo único no se ha producido un truncamiento de dígitos enteros<br /><br /> Conversión produjo un truncamiento de dígitos enteros|N/D<br /><br /> 22003|  
|SQL_INTERVAL_MONTH<br /><br /> SQL_INTERVAL_YEAR<br /><br /> SQL_INTERVAL_YEAR_TO_MONTH|Valor de datos se convirtió sin truncamiento de los campos<br /><br /> Uno o varios campos de valor de datos se puede truncar durante la conversión|N/D<br /><br /> 22015|  
  
 [a] tipos de datos interval todas C se pueden convertir a un tipo de datos de caracteres.  
  
 [b] si el campo tipo de la estructura de intervalo es tal que el intervalo es un único campo (SQL_YEAR o SQL_MONTH), se puede convertir el tipo de intervalo de C para cualquier valor numérico exacto (SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_DECIMAL o SQL_NUMERIC).  
  
 La conversión predeterminada de un intervalo de tipo C es el intervalo de meses del año correspondiente tipo SQL.  
  
 El controlador omite el valor de longitud/indicador al convertir los datos del tipo de datos C de intervalo y se da por supuesto que el tamaño del búfer de datos es el tamaño del tipo de datos C de intervalo. El valor de longitud/indicador se pasa en el *StrLen_or_Ind* argumento en **SQLPutData** y en el búfer especificado con el *StrLen_or_IndPtr* argumento en **SQLBindParameter**. El búfer de datos se especifica con el *DataPtr* argumento en **SQLPutData** y *ParameterValuePtr* argumento en **SQLBindParameter**.
