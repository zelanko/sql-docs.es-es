---
title: 'C a SQL: Tiempo ? Microsoft Docs'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 264ce7751072b79163923f0c141542680f7b02bb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304771"
---
# <a name="c-to-sql-time"></a>C a SQL: Time
El identificador para el tipo de datos ODBC C es:  
  
 SQL_C_TYPE_TIME  
  
 En la tabla siguiente se muestran los tipos de datos SQL ODBC a los que se pueden convertir datos de C de tiempo. Para obtener una explicación de las columnas y los términos de la tabla, vea [Convertir datos de C a tipos](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)de datos SQL .  
  
|Identificador de tipo SQL|Prueba|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Longitud de bytes de columna >8<br /><br /> Longitud de bytes de columna < 8<br /><br /> El valor de los datos no es un momento válido|N/D<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|La longitud de los caracteres de la columna >8<br /><br /> Longitud del carácter de columna < 8<br /><br /> El valor de los datos no es un momento válido|N/D<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_TIME|El valor de los datos es un tiempo válido<br /><br /> El valor de los datos no es un momento válido|N/D<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|El valor de datos es un tiempo válido[a]<br /><br /> El valor de los datos no es un momento válido|N/D<br /><br /> 22007|  
  
 [a] La parte de fecha de la marca de tiempo se establece en la fecha actual y la parte de fracciones de segundo de la marca de tiempo se establece en cero.  
  
 Para obtener información acerca de qué valores son válidos en una estructura de SQL_C_TYPE_TIME, vea Tipos de datos de [C](../../../odbc/reference/appendixes/c-data-types.md), anteriormente en este apéndice.  
  
 Cuando los datos de tiempo C se convierten en datos SQL de caracteres, los datos de caracteres resultantes están en el formato "*hh*:*mm*:*ss*".  
  
 El controlador omite el valor de longitud/indicador al convertir datos del tipo de datos De tiempo C y asume que el tamaño del búfer de datos es el tamaño del tipo de datos C de tiempo. El valor de longitud/indicador se pasa en el argumento *StrLen_or_Ind* en **SQLPutData** y en el búfer especificado con el argumento *StrLen_or_IndPtr* en **SQLBindParameter**. El búfer de datos se especifica con el *argumento DataPtr* en **SQLPutData** y el argumento *ParameterValuePtr* en **SQLBindParameter**.
