---
title: 'C a SQL: GUID | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5863935ddf595409d48be79dc646c0994ddeb0b8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68019326"
---
# <a name="c-to-sql-guid"></a>C a SQL: GUID
El identificador para el tipo de datos C de ODBC GUID es:  
  
 SQL_C_GUID  
  
 La siguiente tabla muestra los tipos de datos a la que se pueden convertir los datos de GUID C de ODBC SQL. Para obtener una explicación de las columnas y los términos de la tabla, vea [convertir datos de C a tipos de datos SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificador de tipo SQL|Prueba|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR|Longitud de bytes de la columna > = 36|N/D|  
|SQL_VARCHAR|Columna de bytes de longitud < 36|22001|  
|SQL_LONGVARCHAR|Valor de datos no es un GUID válido|22018|  
|SQL_WCHAR|Longitud de caracteres de la columna > = 36|N/D|  
|SQL_WVARCHAR|Columna de caracteres de longitud < 36|22001|  
|SQL_WLONGVARCHAR|Valor de datos no es un GUID válido|22018|  
|SQL_GUID|[A] ninguno|N/D|  
  
 [a] todos los valores hexadecimales son válidos como un GUID.  
  
 El controlador omite el valor de longitud/indicador al convertir los datos del tipo de datos GUID C y se da por supuesto que el tamaño del búfer de datos es el tamaño del tipo de datos GUID C. El valor de longitud/indicador se pasa en el *StrLen_or_Ind* argumento en **SQLPutData** y en el búfer especificado con el *StrLen_or_IndPtr* argumento en **SQLBindParameter**. El búfer de datos se especifica con el *DataPtr* argumento en **SQLPutData** y *ParameterValuePtr* argumento en **SQLBindParameter**.
