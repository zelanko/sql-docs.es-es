---
title: 'C a SQL: Tiempo | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from C to SQL types [ODBC], time
- time data type [ODBC]
- converting data from c to SQL types [ODBC], time
ms.assetid: a8da43c9-d9a5-45e5-bd9a-1dd633db2ee0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7ea11803847505698ea42d13727b6177f3a24bda
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63316530"
---
# <a name="c-to-sql-time"></a>C a SQL: Time
El identificador para el tipo de datos ODBC C de tiempo es:  
  
 SQL_C_TYPE_TIME  
  
 La siguiente tabla muestra los tipos de datos a la que se pueden convertir los datos en tiempo de C de ODBC SQL. Para obtener una explicación de las columnas y los términos de la tabla, vea [convertir datos de C a tipos de datos SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificador de tipo SQL|Prueba|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Longitud de bytes de la columna > = 8<br /><br /> Columna de bytes de longitud < 8<br /><br /> Valor de datos no es una hora válida|n/d<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Longitud de caracteres de la columna > = 8<br /><br /> Columna de caracteres de longitud < 8<br /><br /> Valor de datos no es una hora válida|n/d<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_TIME|Valor de datos es una hora válida<br /><br /> Valor de datos no es una hora válida|n/d<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|Valor de datos es una hora válida [a]<br /><br /> Valor de datos no es una hora válida|n/d<br /><br /> 22007|  
  
 [a] de la fecha en la parte de la marca de tiempo se establece en la fecha actual y los segundos fraccionarios parte de la marca de tiempo se establece en cero.  
  
 Para obtener información acerca de qué valores son válidos en una estructura SQL_C_TYPE_TIME, consulte [tipos de datos C](../../../odbc/reference/appendixes/c-data-types.md), anteriormente en este apéndice.  
  
 Cuando los datos en tiempo de C se convierten en datos de SQL de caracteres, los datos de caracteres resultante están en la "*hh*:*mm*:*ss*" formato.  
  
 El controlador omite el valor de longitud/indicador al convertir los datos desde el momento en el tipo de datos de C y se da por supuesto que el tamaño del búfer de datos es el tamaño del tipo de datos C de tiempo. El valor de longitud/indicador se pasa en el *StrLen_or_Ind* argumento en **SQLPutData** y en el búfer especificado con el *StrLen_or_IndPtr* argumento en **SQLBindParameter**. El búfer de datos se especifica con el *DataPtr* argumento en **SQLPutData** y *ParameterValuePtr* argumento en **SQLBindParameter**.
