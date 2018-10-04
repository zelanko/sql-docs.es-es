---
title: Función de conversión de SQL-92 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db5077b9df2673593b6eaec9622aafd1d2c77234
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47753993"
---
# <a name="sql-92-cast-function"></a>Función CAST de SQL-92
El **CAST** es equivalente a la función definida en SQL-92 el **convertir** función definida en ODBC. La sintaxis de las funciones equivalentes es como sigue:  
  
```  
{ fn CONVERT (value-exp, data-type) } /* ODBC  
CAST (value-exp AS data-type) /* SQL92  
```  
  
 SQL-92 **CAST** función exige que los tipos de datos pueden convertirse a qué otros tipos de datos. (Para obtener más información, vea la especificación de SQL-92). El **CAST** se admite la función en el nivel de FIPS transitorio.  
  
 Una aplicación puede determinar la compatibilidad con la **CAST** funcione como se indica a continuación:  
  
1.  Llame a **SQLGetInfo** con el tipo de información SQL_SQL_CONFORMANCE. Si el valor devuelto para el tipo de información es SQL_SC_FIPS127_2_TRANSITIONAL, SQL_SC_SQL92_INTERMEDIATE o SQL_SC_SQL92_FULL, el **CAST** se admite la función.  
  
2.  Si el valor devuelto del tipo de información SQL_SQL_CONFORMANCE es SQL_SC_ENTRY_LEVEL o 0, llame a **SQLGetInfo** con el tipo de información SQL_SQL92_VALUE_EXPRESSIONS. Si se establece el bit SQL_SVE_CAST, el **CAST** se admite la función.
