---
title: 'C a SQL: Fecha ? Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- date data type [ODBC]
- converting data from c to SQL types [ODBC], date
- data conversions from C to SQL types [ODBC], date
ms.assetid: bea087d3-911f-418b-b483-d2b5b334da19
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fa3df8aaee03472076b3241cb9bb60e2a307e28b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298853"
---
# <a name="c-to-sql-date"></a>C a SQL: Date
El identificador del tipo de datos ODBC C de fecha es:  
  
 SQL_C_TYPE_DATE  
  
 En la tabla siguiente se muestran los tipos de datos SQL ODBC a los que se pueden convertir los datos de fecha C. Para obtener una explicación de las columnas y los términos de la tabla, vea [Convertir datos de C a tipos](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)de datos SQL .  
  
|Identificador de tipo SQL|Prueba|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Longitud de los bytes de columna >10<br /><br /> Longitud de byte de columna < 10<br /><br /> El valor de los datos no es una fecha válida|N/D<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|La longitud de los caracteres de la columna >10<br /><br /> Longitud del carácter de columna < 10<br /><br /> El valor de los datos no es una fecha válida|N/D<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|El valor de los datos es una fecha válida<br /><br /> El valor de los datos no es una fecha válida|N/D<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|El valor de datos es una fecha válida[a]<br /><br /> El valor de los datos no es una fecha válida|N/D<br /><br /> 22007|  
  
 [a] La parte de tiempo de la marca de tiempo se establece en cero.  
  
 Para obtener información acerca de qué valores son válidos en una estructura de SQL_C_TYPE_DATE, vea Tipos de datos de [C](../../../odbc/reference/appendixes/c-data-types.md), anteriormente en este apéndice.  
  
 Cuando los datos de fecha C se convierten en datos SQL de caracteres, los datos de caracteres resultantes están en el formato "*aaaa*-*mm*-*dd*".  
  
 El controlador omite el valor de longitud/indicador al convertir datos del tipo de datos de fecha C y supone que el tamaño del búfer de datos es el tamaño del tipo de datos de fecha C. El valor de longitud/indicador se pasa en el argumento *StrLen_or_Ind* en **SQLPutData** y en el búfer especificado con el argumento *StrLen_or_IndPtr* en **SQLBindParameter**. El búfer de datos se especifica con el *argumento DataPtr* en **SQLPutData** y el argumento *ParameterValuePtr* en **SQLBindParameter**.
