---
title: 'C a SQL: Numérico ? Microsoft Docs'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bbc0a994ef95f2deca29c8a4cbb06f3167b0433f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304736"
---
# <a name="c-to-sql-numeric"></a>C a SQL: Numeric
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
  
 En la tabla siguiente se muestran los tipos de datos SQL ODBC a los que se pueden convertir datos numéricos de C. Para obtener una explicación de las columnas y los términos de la tabla, vea [Convertir datos de C a tipos](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)de datos SQL .  
  
|Identificador de tipo SQL|Prueba|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Número de dígitos <- Longitud de bytes de columna<br /><br /> Número de dígitos > longitud de bytes de columna|N/D<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Número de caracteres <- Longitud de caracteres de columna<br /><br /> Número de caracteres > Longitud de caracteres de columna|N/D<br /><br /> 22001|  
|SQL_DECIMAL[b]<br /><br /> SQL_NUMERIC[b]<br /><br /> SQL_TINYINT[b]<br /><br /> SQL_SMALLINT[b]<br /><br /> SQL_INTEGER[b]<br /><br /> SQL_BIGINT[b]|Datos convertidos sin truncamiento o con dígitos fraccionarios truncados<br /><br /> Datos convertidos con truncamiento de dígitos enteros|N/D<br /><br /> 22003|  
|SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE|Los datos están dentro del rango del tipo de datos al que se está convirtiendo el número<br /><br /> Los datos están fuera del rango del tipo de datos al que se está convirtiendo el número|N/D<br /><br /> 22003|  
|SQL_BIT|Los datos son 0 o 1<br /><br /> Los datos son mayores que 0, menos que 2, y no iguales a 1<br /><br /> Los datos son menores o mayores o iguales que 2|N/D<br /><br /> 22001<br /><br /> 22003|  
|SQL_INTERVAL_YEAR[a]<br /><br /> SQL_INTERVAL_MONTH[a]<br /><br /> SQL_INTERVAL_DAY[a]<br /><br /> SQL_INTERVAL_HOUR[a]<br /><br /> SQL_INTERVAL_MINUTE[a]<br /><br /> SQL_INTERVAL_SECOND[a]|Datos no truncados.<br /><br /> Datos truncados.|N/D<br /><br /> 22015|  
  
 [a] Estas conversiones solo se admiten para los tipos de datos numéricos exactos (SQL_C_STINYINT, SQL_C_UTINYINT, SQL_C_SSHORT, SQL_C_USHORT, SQL_C_SLONG, SQL_C_ULONG o SQL_C_NUMERIC). No se admiten para los tipos de datos numéricos aproximados (SQL_C_FLOAT o SQL_C_DOUBLE). Los tipos de datos numéricos exactos de C no se pueden convertir en un tipo SQL de intervalo cuya precisión de intervalo no sea un solo campo.  
  
 [b] Para el caso "n/a", un controlador puede devolver opcionalmente SQL_SUCCESS_WITH_INFO y 01S07 cuando hay un truncamiento fraccionario.  
  
 El controlador omite el valor de longitud/indicador al convertir datos de los tipos de datos numéricos de C y supone que el tamaño del búfer de datos es el tamaño del tipo de datos C numérico. El valor de longitud/indicador se pasa en el argumento *StrLen_or_Ind* en **SQLPutData** y en el búfer especificado con el argumento *StrLen_or_IndPtr* en **SQLBindParameter**. El búfer de datos se especifica con el *argumento DataPtr* en **SQLPutData** y el argumento *ParameterValuePtr* en **SQLBindParameter**.
