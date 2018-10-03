---
title: 'C a SQL: numérico | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- numeric data type [ODBC], converting
- data conversions from C to SQL types [ODBC], numeric
- converting data from c to SQL types [ODBC], numeric
ms.assetid: af4095ff-06c3-4b04-83bf-19f9ee098dc2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 816394bb8469148504c1b2b416e77fec814bef8f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47786673"
---
# <a name="c-to-sql-numeric"></a>C a SQL: numérico
Los identificadores para los tipos de datos ODBC C numéricos son:  
  
 SQL_C_STINYINT  
  
 SQL_C_SLONG  
  
 SQL_C_UTINYINT  
  
 SQL_C_ULONG  
  
 SQL_C_TINYINT  
  
 SQL_C_LONG  
  
 SQL_C_SSHORT  
  
 SQL_C_FLOAT  
  
 SQL_C_USHORT  
  
 SQL_C_DOUBLE  
  
 SQL_C_SHORT  
  
 SQL_C_NUMERIC  
  
 SQL_C_SBIGINT  
  
 SQL_C_UBIGINT  
  
 La siguiente tabla muestra los tipos de datos a la que se pueden convertir datos numéricos de C de ODBC SQL. Para obtener una explicación de las columnas y los términos de la tabla, vea [convertir datos de C a tipos de datos SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificador de tipo SQL|Prueba|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Número de dígitos < = longitud de bytes de la columna<br /><br /> Número de dígitos > longitud de bytes de la columna|n/d<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Número de caracteres < = longitud de caracteres de la columna<br /><br /> Número de caracteres > longitud de caracteres de la columna|n/d<br /><br /> 22001|  
|SQL_DECIMAL [b]<br /><br /> SQL_NUMERIC [b]<br /><br /> SQL_TINYINT [b]<br /><br /> SQL_SMALLINT [b]<br /><br /> SQL_INTEGER [b]<br /><br /> SQL_BIGINT [b]|Convierten sin truncamiento de datos o con truncan de dígitos fraccionarios<br /><br /> Convierten datos con el truncamiento de dígitos enteros|n/d<br /><br /> 22003|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|Datos están dentro del intervalo del tipo de datos a la que se va a convertir el número<br /><br /> Datos están fuera del intervalo del tipo de datos a la que se va a convertir el número|n/d<br /><br /> 22003|  
|SQL_BIT|Datos están 0 o 1<br /><br /> Datos están mayores que 0, inferior a 2 y no es igual a 1<br /><br /> Datos están menor que 0 o mayor que o igual a 2|n/d<br /><br /> 22001<br /><br /> 22003|  
|SQL_INTERVAL_YEAR [a]<br /><br /> SQL_INTERVAL_MONTH [a]<br /><br /> SQL_INTERVAL_DAY [a]<br /><br /> SQL_INTERVAL_HOUR [a]<br /><br /> SQL_INTERVAL_MINUTE [a]<br /><br /> SQL_INTERVAL_SECOND [a]|No se truncan los datos.<br /><br /> Datos truncados.|n/d<br /><br /> 22015|  
  
 [a] estas conversiones se admiten únicamente para los tipos de datos numéricos exactos (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_SSHORT, SQL_C_USHORT, SQL_C_SLONG, SQL_C_ULONG o SQL_C_NUMERIC). No se admiten para los tipos de datos numéricos aproximados (SQL_C_FLOAT o SQL_C_DOUBLE). No se puede convertir tipos de datos C numéricos exactos para un tipo SQL cuya precisión de intervalo no es un único campo de intervalo.  
  
 [b] para el caso de "n/a", un controlador puede opcionalmente devolver SQL_SUCCESS_WITH_INFO y 01S07 cuando hay un truncamiento fraccionario.  
  
 El controlador omite el valor de longitud/indicador al convertir datos de los tipos de datos numéricos de C y se da por supuesto que el tamaño del búfer de datos es el tamaño del tipo de datos C numérico. El valor de longitud/indicador se pasa en el *StrLen_or_Ind* argumento en **SQLPutData** y en el búfer especificado con el *StrLen_or_IndPtr* argumento en **SQLBindParameter**. El búfer de datos se especifica con el *DataPtr* argumento en **SQLPutData** y *ParameterValuePtr* argumento en **SQLBindParameter**.
