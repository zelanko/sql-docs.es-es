---
title: 'C a SQL: tiempo | Microsoft Docs'
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
ms.openlocfilehash: c4a3734ff8d9f0cb120e1d33433ee3a301bb59ae
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68019300"
---
# <a name="c-to-sql-time"></a>C a SQL: hora
El identificador para el tipo de datos de tiempo ODBC C es:  
  
 SQL_C_TYPE_TIME  
  
 En la tabla siguiente se muestran los tipos de datos de ODBC SQL en los que se pueden convertir los datos de C. Para obtener una explicación de las columnas y los términos de la tabla, vea [convertir datos de C a tipos de datos de SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificador de tipo de SQL|Prueba|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Longitud de bytes de columna >= 8<br /><br /> Longitud de bytes de columna < 8<br /><br /> El valor de los datos no es una hora válida|N/D<br /><br /> 22001<br /><br /> 22008|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Longitud de caracteres de columna >= 8<br /><br /> Longitud de caracteres de columna < 8<br /><br /> El valor de los datos no es una hora válida|N/D<br /><br /> 22001<br /><br /> 22008|  
|SQL_TYPE_TIME|El valor de los datos es una hora válida<br /><br /> El valor de los datos no es una hora válida|N/D<br /><br /> 22007|  
|SQL_TYPE_TIMESTAMP|El valor de los datos es una hora válida [a]<br /><br /> El valor de los datos no es una hora válida|N/D<br /><br /> 22007|  
  
 [a] la parte de fecha de la marca de tiempo se establece en la fecha actual y la parte de fracciones de segundo de la marca de tiempo se establece en cero.  
  
 Para obtener información sobre qué valores son válidos en una estructura de SQL_C_TYPE_TIME, vea [tipos de datos de C](../../../odbc/reference/appendixes/c-data-types.md), anteriormente en este apéndice.  
  
 Cuando los datos de tiempo C se convierten en datos SQL de caracteres, los datos de caracteres resultantes tienen el formato "*HH*:*mm*:*SS*".  
  
 El controlador omite el valor de longitud/indicador al convertir los datos del tipo de datos Time C y da por supuesto que el tamaño del búfer de datos es el tamaño del tipo de datos Time de C. El valor de longitud/indicador se pasa en el argumento *StrLen_or_Ind* de **SQLPutData** y en el búfer especificado con el argumento *StrLen_or_IndPtr* en **SQLBindParameter**. El búfer de datos se especifica con el argumento *DataPtr* en **SQLPutData** y el argumento *ParameterValuePtr* en **SQLBindParameter**.
