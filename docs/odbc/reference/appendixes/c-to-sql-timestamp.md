---
title: 'C a SQL: Marca de tiempo ? Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data conversions from C to SQL types [ODBC], timestamp
- timestamp data type [ODBC]
- converting data from c to SQL types [ODBC], timestamp
ms.assetid: 0e08bfff-68f9-4648-9558-09b57fea08ad
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3102e5043527a1aa9463980c9dd546839cb92f37
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81283755"
---
# <a name="c-to-sql-timestamp"></a>C a SQL: Timestamp
El identificador del tipo de datos ODBC C de marca de tiempo es:  
  
 SQL_C_TYPE_TIMESTAMP  
  
 En la tabla siguiente se muestran los tipos de datos SQL ODBC a los que se pueden convertir los datos de marca de tiempo C. Para obtener una explicación de las columnas y los términos de la tabla, vea [Convertir datos de C a tipos](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)de datos SQL .  
  
|Identificador de tipo SQL|Prueba|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Longitud de bytes de columna >- Longitud de byte de caracteres<br /><br /> 19 <- Longitud de bytes de columna < Longitud de byte de caracteres<br /><br /> Longitud de bytes de columna < 19<br /><br /> El valor de los datos no es una marca de tiempo válida|N/D<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Longitud de caracteres de columna >- Longitud de caracteres de datos<br /><br /> 19 <- Longitud del carácter de columna < Longitud de caracteres de los datos<br /><br /> Longitud del carácter de columna < 19<br /><br /> El valor de los datos no es una marca de tiempo válida|N/D<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|Los campos de tiempo son cero<br /><br /> Los campos de tiempo son distintos de cero<br /><br /> El valor de los datos no contiene una fecha válida|N/D<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIME|Los campos de segundos fraccionarios son cero[a]<br /><br /> Los campos de fracciones de segundo son distintos de cero[a]<br /><br /> El valor de los datos no contiene un tiempo válido|N/D<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|Los campos de fracciones de segundo no se truncan<br /><br /> Los campos de fracciones de segundo se truncan<br /><br /> El valor de los datos no es una marca de tiempo válida|N/D<br /><br /> 22008<br /><br /> 22007|  
  
 [a] Se omiten los campos de fecha de la estructura de marca de tiempo.  
  
 Para obtener información acerca de qué valores son válidos en una estructura de SQL_C_TIMESTAMP, vea Tipos de [datos de C](../../../odbc/reference/appendixes/c-data-types.md), anteriormente en este apéndice.  
  
 Cuando los datos de marca de tiempo C se convierten en datos SQL de caracteres, los datos de caracteres resultantes se encuentra en el "*aaaa*-*mm*-*dd* *hh*:*mm*:*ss*[.* f...*]" Formato.  
  
 El controlador omite el valor de longitud/indicador al convertir datos del tipo de datos C de marca de tiempo y asume que el tamaño del búfer de datos es el tamaño del tipo de datos C de marca de tiempo. El valor de longitud/indicador se pasa en el argumento *StrLen_or_Ind* en **SQLPutData** y en el búfer especificado con el argumento *StrLen_or_IndPtr* en **SQLBindParameter**. El búfer de datos se especifica con el *argumento DataPtr* en **SQLPutData** y el argumento *ParameterValuePtr* en **SQLBindParameter**.
