---
title: 'C a SQL: fecha | Documentos de Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- date data type [ODBC]
- converting data from c to SQL types [ODBC], date
- data conversions from C to SQL types [ODBC], date
ms.assetid: bea087d3-911f-418b-b483-d2b5b334da19
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0c14da46be67b8b945f167f408dd15005514e013
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="c-to-sql-date"></a>C a SQL: fecha
El identificador para el tipo de datos de fecha ODBC C es:  
  
 SQL_C_TYPE_DATE  
  
 La siguiente tabla muestra los tipos de datos a la que se puede convertir fecha datos C de ODBC SQL. Para obtener una explicación de las columnas y los términos de la tabla, vea [convertir datos de C a tipos de datos de SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificador de tipo SQL|Prueba|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Longitud de bytes de la columna > = 10<br /><br /> Columna de longitud de bytes < 10<br /><br /> Valor de datos no es una fecha válida|n/d<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Longitud de caracteres de la columna > = 10<br /><br /> Columna de caracteres de longitud < 10<br /><br /> Valor de datos no es una fecha válida|n/d<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|Valor de datos es una fecha válida<br /><br /> Valor de datos no es una fecha válida|n/d<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|Valor de datos es una fecha válida [a]<br /><br /> Valor de datos no es una fecha válida|n/d<br /><br /> 22007|  
  
 [a] la parte de hora de la marca de tiempo se establece en cero.  
  
 Para obtener información acerca de qué valores son válidos en una estructura SQL_C_TYPE_DATE, consulte [tipos de datos C](../../../odbc/reference/appendixes/c-data-types.md), anteriormente en este apéndice.  
  
 Cuando los datos de fecha C se convierte en datos de SQL de caracteres, los datos de caracteres resultante están en la "*aaaa*-*mm*-*dd*" formato.  
  
 El controlador omite el valor de longitud/indicador al convertir datos de tipo de datos date C y se da por supuesto que el tamaño del búfer de datos es el tamaño del tipo de datos date C. El valor de longitud/indicador se pasa en el *StrLen_or_Ind* argumento en **SQLPutData** y en el búfer especificado con el *StrLen_or_IndPtr* argumento en **SQLBindParameter**. El búfer de datos se especifica con el *DataPtr* argumento en **SQLPutData** y *ParameterValuePtr* argumento en **SQLBindParameter**.
