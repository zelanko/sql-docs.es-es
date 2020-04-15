---
title: 'C a SQL: GUID ? Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from c to SQL types [ODBC], guid
- data conversions from C to SQL types [ODBC], guid
- GUID data type [ODBC]
ms.assetid: 9168b0b6-a828-4fef-b8cd-bdf439776f23
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b3b559499273e885e23da10d9093a0ce9ff92393
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306626"
---
# <a name="c-to-sql-guid"></a>C a SQL: GUID
El identificador del tipo de datos GUID ODBC C es:  
  
 SQL_C_GUID  
  
 En la tabla siguiente se muestran los tipos de datos SQL ODBC a los que se pueden convertir los datos GUID C. Para obtener una explicación de las columnas y los términos de la tabla, vea [Convertir datos de C a tipos](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)de datos SQL .  
  
|Identificador de tipo SQL|Prueba|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR|La longitud de los bytes de columna >36|N/D|  
|SQL_VARCHAR|Longitud de bytes de columna < 36|22001|  
|SQL_LONGVARCHAR|El valor de datos no es un GUID válido|22018|  
|SQL_WCHAR|La longitud de los caracteres de la columna >36|N/D|  
|SQL_WVARCHAR|Longitud del carácter de columna < 36|22001|  
|SQL_WLONGVARCHAR|El valor de datos no es un GUID válido|22018|  
|SQL_GUID|Ninguno[a]|N/D|  
  
 [a] Todos los valores hexidecimales son válidos como GUID.  
  
 El controlador omite el valor de longitud/indicador al convertir datos del tipo de datos GUID C y supone que el tamaño del búfer de datos es el tamaño del tipo de datos GUID C. El valor de longitud/indicador se pasa en el argumento *StrLen_or_Ind* en **SQLPutData** y en el búfer especificado con el argumento *StrLen_or_IndPtr* en **SQLBindParameter**. El búfer de datos se especifica con el *argumento DataPtr* en **SQLPutData** y el argumento *ParameterValuePtr* en **SQLBindParameter**.
