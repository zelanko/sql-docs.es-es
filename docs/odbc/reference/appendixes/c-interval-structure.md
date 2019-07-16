---
title: Estructura de intervalo de C | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- interval data type [ODBC], structure
- C data types [ODBC], interval
ms.assetid: 52b42b56-50aa-4ce6-8d79-0963c7a71437
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3387b4fa48eb1a04102daadcc08f971765d7ca2b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68037783"
---
# <a name="c-interval-structure"></a>Estructura de intervalo de C
Cada uno de los tipos de datos del intervalo de C se enumeran en la [tipos de datos C](../../../odbc/reference/appendixes/c-data-types.md) sección usa la misma estructura que contiene el intervalo de datos. Cuando **SQLFetch**, **SQLFetchScroll**, o **SQLGetData** es llama, el controlador devuelve datos en la estructura SQL_INTERVAL_STRUCT, utiliza el valor que se especificó en el aplicación para los tipos de datos de C (en la llamada a **SQLBindCol**, **SQLGetData**, o **SQLBindParameter**) para interpretar el contenido de SQL_INTERVAL_STRUCT y rellena la *interval_type* campo de la estructura con la *enum* corresponde al tipo C de valor. Tenga en cuenta que los controladores no leen la *interval_type* campo para determinar el tipo del intervalo; recuperarán el valor del campo descriptor SQL_DESC_CONCISE_TYPE. Cuando se usa la estructura de datos del parámetro, el controlador utiliza el valor especificado por la aplicación en el campo SQL_DESC_CONCISE_TYPE del APD para interpretar el contenido de SQL_INTERVAL_STRUCT, incluso si la aplicación establece el valor de la  *interval_type* campo en un valor diferente.  
  
 Esta estructura se define como sigue:  
  
```  
typedef struct tagSQL_INTERVAL_STRUCT  
{  
   SQLINTERVAL interval_type;   
   SQLSMALLINT interval_sign;  
   union {  
         SQL_YEAR_MONTH_STRUCT   year_month;  
         SQL_DAY_SECOND_STRUCT   day_second;  
         } intval;  
} SQL_INTERVAL_STRUCT;  
typedef enum   
{  
   SQL_IS_YEAR = 1,  
   SQL_IS_MONTH = 2,  
   SQL_IS_DAY = 3,  
   SQL_IS_HOUR = 4,  
   SQL_IS_MINUTE = 5,  
   SQL_IS_SECOND = 6,  
   SQL_IS_YEAR_TO_MONTH = 7,  
   SQL_IS_DAY_TO_HOUR = 8,  
   SQL_IS_DAY_TO_MINUTE = 9,  
   SQL_IS_DAY_TO_SECOND = 10,  
   SQL_IS_HOUR_TO_MINUTE = 11,  
   SQL_IS_HOUR_TO_SECOND = 12,  
   SQL_IS_MINUTE_TO_SECOND = 13  
} SQLINTERVAL;  
  
typedef struct tagSQL_YEAR_MONTH  
{  
   SQLUINTEGER year;  
   SQLUINTEGER month;   
} SQL_YEAR_MONTH_STRUCT;  
  
typedef struct tagSQL_DAY_SECOND  
{  
   SQLUINTEGER day;  
   SQLUINTEGER hour;  
   SQLUINTEGER minute;  
   SQLUINTEGER second;  
   SQLUINTEGER fraction;  
} SQL_DAY_SECOND_STRUCT;  
```  
  
 El *interval_type* campo de la SQL_INTERVAL_STRUCT indica a la aplicación qué estructura se mantiene en la unión y también qué miembros de la estructura son relevantes. El *interval_sign* campo tiene el valor SQL_FALSE si el intervalo inicial de campo es sin signo; si es SQL_TRUE, el campo inicial es negativo. El valor en el propio campo inicial siempre es sin signo, independientemente del valor de *interval_sign*. El *interval_sign* campo actúa como un bit de signo.
