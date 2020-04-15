---
title: 'SQL a C: Bit ? Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to c types [ODBC], bit
- bit data type [ODBC]
- data conversions from SQL to C types [ODBC], bit
ms.assetid: 0eeaab8b-ad82-4a36-b464-9a1211d5f72c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 57688f34c504b221f77c1b66792bf9ee9398df27
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296755"
---
# <a name="sql-to-c-bit"></a>SQL a C: bit
El identificador del tipo de datos SQL ODBC de bits es:  
  
 SQL_BIT  
  
 En la tabla siguiente se muestran los tipos de datos ODBC C a los que se pueden convertir datos SQL de bits. Para obtener una explicación de las columnas y los términos de la tabla, vea [Convertir datos de SQL a tipos](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md)de datos C .  
  
|Identificador de tipo C|Prueba|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR<br /><br /> SQL_C_WCHAR|*BufferLength* > 1<br /><br /> *BufferLongitud* <1|data<br /><br /> No definido|1<br /><br /> No definido|N/D<br /><br /> 22003|  
|SQL_C_STINYINT<br /><br /> SQL_C_UTINYINT<br /><br /> SQL_C_TINYINT<br /><br /> SQL_C_SBIGINT<br /><br /> SQL_C_UBIGINT<br /><br /> SQL_C_SSHORT<br /><br /> SQL_C_USHORT<br /><br /> SQL_C_SHORT<br /><br /> SQL_C_SLONG<br /><br /> SQL_C_ULONG<br /><br /> SQL_C_LONG<br /><br /> SQL_C_FLOAT<br /><br /> SQL_C_DOUBLE<br /><br /> SQL_C_NUMERIC|Ninguno[a]|data|Tamaño del tipo de datos C|N/D|  
|SQL_C_BIT|Ninguno[a]|data|1[b]|N/D|  
|SQL_C_BINARY|*BufferLongitud* >1<br /><br /> *BufferLength* < 1|data<br /><br /> No definido|1<br /><br /> No definido|N/D<br /><br /> 22003|  
  
 [a] El valor de *BufferLength* se omite para esta conversión. El controlador supone que el tamaño de **TargetValuePtr* es el tamaño del tipo de datos C.  
  
 [b] Este es el tamaño del tipo de datos C correspondiente.  
  
 Cuando los datos SQL de bits se convierten en datos de caracteres C, los valores posibles son "0" y "1".
