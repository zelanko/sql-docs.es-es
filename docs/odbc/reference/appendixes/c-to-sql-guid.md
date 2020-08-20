---
description: 'C a SQL: GUID'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3fca2ba20df65222eaf1ce6f4384f449a1524334
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499988"
---
# <a name="c-to-sql-guid"></a>C a SQL: GUID
El identificador para el tipo de datos de GUID de C ODBC es:  
  
 SQL_C_GUID  
  
 En la tabla siguiente se muestran los tipos de datos de ODBC SQL en los que se pueden convertir los datos de GUID C. Para obtener una explicación de las columnas y los términos de la tabla, vea [convertir datos de C a tipos de datos de SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|Identificador de tipo de SQL|Prueba|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR|Longitud de bytes de columna >= 36|N/D|  
|SQL_VARCHAR|Longitud de bytes de columna < 36|22001|  
|SQL_LONGVARCHAR|El valor de los datos no es un GUID válido|22018|  
|SQL_WCHAR|Longitud de caracteres de columna >= 36|N/D|  
|SQL_WVARCHAR|Longitud de caracteres de columna < 36|22001|  
|SQL_WLONGVARCHAR|El valor de los datos no es un GUID válido|22018|  
|SQL_GUID|Ninguno [a]|N/D|  
  
 [a] todos los valores hexadecimales son válidos como un GUID.  
  
 El controlador omite el valor de longitud/indicador al convertir los datos del tipo de datos GUID C y da por supuesto que el tamaño del búfer de datos es el tamaño del tipo de datos GUID C. El valor de longitud/indicador se pasa en el argumento *StrLen_or_Ind* de **SQLPutData** y en el búfer especificado con el argumento *StrLen_or_IndPtr* en **SQLBindParameter**. El búfer de datos se especifica con el argumento *DataPtr* en **SQLPutData** y el argumento *ParameterValuePtr* en **SQLBindParameter**.
