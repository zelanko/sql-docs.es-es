---
title: 'C a SQL: marca de tiempo | Documentos de Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data conversions from C to SQL types [ODBC], timestamp
- timestamp data type [ODBC]
- converting data from c to SQL types [ODBC], timestamp
ms.assetid: 0e08bfff-68f9-4648-9558-09b57fea08ad
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc9202f97100e2b6eb69776d7864c8bafbed20d8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32905900"
---
# <a name="c-to-sql-timestamp"></a>C a SQL: marca de tiempo
El identificador para el tipo de datos ODBC C de marca de tiempo es:  
  
 SQL_C_TYPE_TIMESTAMP  
  
 La siguiente tabla muestra los tipos de datos a la que se pueden convertir los datos de marca de tiempo C de ODBC SQL. Para obtener una explicación de las columnas y los términos de la tabla, vea [convertir datos de C a tipos de datos de SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificador de tipo SQL|Prueba|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Longitud de bytes de la columna > = longitud de bytes de caracteres<br /><br /> 19 < = longitud de bytes de la columna < longitud de bytes de caracteres<br /><br /> Columna de longitud de bytes < 19<br /><br /> Valor de datos no es una marca de tiempo válida|n/d<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Longitud de caracteres de la columna > = longitud de caracteres de datos<br /><br /> 19 < = longitud de caracteres de la columna < longitud de datos de caracteres<br /><br /> Columna de caracteres de longitud < 19<br /><br /> Valor de datos no es una marca de tiempo válida|n/d<br /><br /> 22001<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_DATE|Campos de hora son cero<br /><br /> Campos de hora son distintos de cero<br /><br /> El valor de datos no contiene una fecha válida|n/d<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIME|Campos de fracciones de segundo son cero [a]<br /><br /> Campos de fracciones de segundo son [a] es distinto de cero<br /><br /> El valor de datos no contiene una hora válida|n/d<br /><br /> 22008<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|No se truncan los campos de fracciones de segundo<br /><br /> Campos de fracciones de segundo se truncan<br /><br /> Valor de datos no es una marca de tiempo válida|n/d<br /><br /> 22008<br /><br /> 22007|  
  
 [La fecha se omiten los campos de la estructura de marca de tiempo a].  
  
 Para obtener información acerca de qué valores son válidos en una estructura SQL_C_TIMESTAMP, consulte [tipos de datos C](../../../odbc/reference/appendixes/c-data-types.md), anteriormente en este apéndice.  
  
 Cuando los datos de marca de tiempo C se convierte en datos de SQL de caracteres, los datos de caracteres resultante están en la "*aaaa*-*mm*-*dd* *hh*:*mm*:*ss*[.*f...*] "formato.  
  
 El controlador omite el valor de longitud/indicador al convertir datos del tipo de datos C de la marca de tiempo y se da por supuesto que el tamaño del búfer de datos es el tamaño del tipo de datos C de la marca de tiempo. El valor de longitud/indicador se pasa en el *StrLen_or_Ind* argumento en **SQLPutData** y en el búfer especificado con el *StrLen_or_IndPtr* argumento en **SQLBindParameter**. El búfer de datos se especifica con el *DataPtr* argumento en **SQLPutData** y *ParameterValuePtr* argumento en **SQLBindParameter**.
