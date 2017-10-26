---
title: "Función de conversión de SQL-92 | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- functions [ODBC], SQL-92 functions
- SQL-92 functions [ODBC]
- CAST function [ODBC]
ms.assetid: 982f09e5-8205-41b9-98b3-8f898e24743f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 8389ff0812c91ca5a35007a21d70a2a1ca0baee8
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sql-92-cast-function"></a>Función de conversión de SQL-92
El **conversión** función definido en SQL-92 es equivalente a la **convertir** función definida en ODBC. La sintaxis de la función equivalente es como sigue:  
  
```  
{ fn CONVERT (value-exp, data-type) } /* ODBC  
CAST (value-exp AS data-type) /* SQL92  
```  
  
 SQL-92 **conversión** exige una función con qué tipos de datos se pueden convertir a qué otros tipos de datos. (Para obtener más información, vea la especificación de SQL-92). El **conversión** se admite la función en el nivel de transición de FIPS.  
  
 Una aplicación puede determinar la compatibilidad con la **conversión** funcione como se indica a continuación:  
  
1.  Llame a **SQLGetInfo** con el tipo de información de SQL_SQL_CONFORMANCE. Si el valor devuelto para el tipo de información es SQL_SC_FIPS127_2_TRANSITIONAL, SQL_SC_SQL92_INTERMEDIATE o SQL_SC_SQL92_FULL, la **conversión** se admite la función.  
  
2.  Si el valor devuelto del tipo de información SQL_SQL_CONFORMANCE es SQL_SC_ENTRY_LEVEL o 0, llame a **SQLGetInfo** con el tipo de información de SQL_SQL92_VALUE_EXPRESSIONS. Si se establece el bit SQL_SVE_CAST, la **conversión** se admite la función.

