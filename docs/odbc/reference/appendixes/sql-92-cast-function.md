---
title: Función DE CAST DE SQL-92 (SQL-92 CAST) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], SQL-92 functions
- SQL-92 functions [ODBC]
- CAST function [ODBC]
ms.assetid: 982f09e5-8205-41b9-98b3-8f898e24743f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 09d2a2de710dafd4e744166c4219f4c903fd3321
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305066"
---
# <a name="sql-92-cast-function"></a>Función CAST de SQL-92
La función **CAST** definida en SQL-92 es equivalente a la función **CONVERT** definida en ODBC. La sintaxis de las funciones equivalentes es la siguiente:  
  
```  
{ fn CONVERT (value-exp, data-type) } /* ODBC  
CAST (value-exp AS data-type) /* SQL92  
```  
  
 La función **CAST** de SQL-92 exige qué tipos de datos se pueden convertir a qué otros tipos de datos. (Para obtener más información, consulte la especificación SQL-92.) La función **CAST** se admite en el nivel de transición FIPS.  
  
 Una aplicación puede determinar la compatibilidad con la función **CAST** de la siguiente manera:  
  
1.  Llame a **SQLGetInfo** con el tipo de información SQL_SQL_CONFORMANCE. Si el valor devuelto para el tipo de información es SQL_SC_FIPS127_2_TRANSITIONAL, SQL_SC_SQL92_INTERMEDIATE o SQL_SC_SQL92_FULL, se admite la función **CAST.**  
  
2.  Si el valor devuelto del tipo de información SQL_SQL_CONFORMANCE es SQL_SC_ENTRY_LEVEL o 0, llame a **SQLGetInfo** con el tipo de información SQL_SQL92_VALUE_EXPRESSIONS. Si se establece el bit SQL_SVE_CAST, se admite la función **CAST.**
