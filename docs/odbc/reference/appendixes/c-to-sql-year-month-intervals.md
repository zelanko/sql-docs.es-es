---
title: "C a SQL: intervalos de mes del año | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- converting data from c to SQL types [ODBC], year-month intervals
- intervals [ODBC], converting
- year-month intervals [ODBC]
- data conversions from C to SQL types [ODBC], year-month intervals
ms.assetid: a0eb7b55-9db0-4375-9210-bddec4593880
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 880564e5883299b5f79df4f0480ab81ae8c9de1c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="c-to-sql-year-month-intervals"></a>C a SQL: intervalos de mes del año
Los identificadores para los tipos de datos ODBC C de mes y año intervalo son:  
  
 SQL_C_INTERVAL_MONTH SQL_C_INTERVAL_YEAR SQL_C_INTERVAL_YEAR_TO_MONTH  
  
 La siguiente tabla muestra en qué mes y año-intervalo C datos se pueden convertir los tipos de datos de ODBC SQL. Para obtener una explicación de las columnas y los términos de la tabla, vea [convertir datos de C a tipos de datos de SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificador de tipo SQL|Prueba|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR [a]<br /><br /> SQL_VARCHAR [a]<br /><br /> SQL_LONGVARCHAR [a]|Longitud de bytes de la columna > = longitud de bytes de caracteres<br /><br /> Longitud de bytes de la columna < [a] longitud de bytes de caracteres<br /><br /> Valor de datos no es un intervalo válido de literal|n/d<br /><br /> 22001<br /><br /> 22015|  
|SQL_WCHAR [a]<br /><br /> SQL_WVARCHAR [a]<br /><br /> SQL_WLONGVARCHAR [a]|Longitud de caracteres de la columna > = longitud de caracteres de datos<br /><br /> Longitud de caracteres de la columna < caracteres de longitud de datos [a]<br /><br /> Valor de datos no es un intervalo válido de literal|n/d<br /><br /> 22001<br /><br /> 22015|  
|SQL_TINYINT [b]<br /><br /> SQL_SMALLINT [b]<br /><br /> SQL_INTEGER [b]<br /><br /> SQL_BIGINT [b]<br /><br /> SQL_NUMERIC [b]<br /><br /> SQL_DECIMAL de ODBC [b]|Conversión de un intervalo de un solo campo no se ha producido truncamiento de dígitos enteros<br /><br /> Conversión produjo truncamiento de dígitos enteros|n/d<br /><br /> 22003|  
|SQL_INTERVAL_MONTH<br /><br /> SQL_INTERVAL_YEAR<br /><br /> SQL_INTERVAL_YEAR_TO_MONTH|Valor de dato se convierte sin truncamiento de los campos<br /><br /> Uno o más campos de valor de datos se truncaron durante la conversión|n/d<br /><br /> 22015|  
  
 [a] tipos de datos interval de todos los C se pueden convertir a un tipo de datos de caracteres.  
  
 [b] si el campo tipo de la estructura de intervalo es tal que el intervalo es de un único campo (SQL_YEAR o SQL_MONTH), se puede convertir el tipo de intervalo C para cualquier valor numérico exacto (SQL_TINYINT, SQL_SMALLINT, SQL_INTEGER, SQL_BIGINT, SQL_DECIMAL o SQL_NUMERIC).  
  
 La conversión de valor predeterminado de un intervalo de tipo C es el intervalo de meses del año correspondiente tipo SQL.  
  
 El controlador omite el valor de longitud/indicador al convertir datos de los tipos de datos interval C y se da por supuesto que el tamaño del búfer de datos es el tamaño del tipo de datos C de intervalo. El valor de longitud/indicador se pasa en el *StrLen_or_Ind* argumento en **SQLPutData** y en el búfer especificado con el *StrLen_or_IndPtr* argumento en **SQLBindParameter**. El búfer de datos se especifica con el *DataPtr* argumento en **SQLPutData** y *ParameterValuePtr* argumento en **SQLBindParameter**.
