---
title: Asignaciones SQLSTATE | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- compatibility [ODBC], SQLSTATE
- backward compatibility [ODBC], SQLSTATE
- SQLSTATE [ODBC]
ms.assetid: 6e6cabcf-a204-40eb-b77d-8a0c4a5e8524
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 68b514cd35e7da713f6e38a01c25d5d64d621794
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="sqlstate-mappings"></a>Asignaciones SQLSTATE
En este tema se trata los valores de SQLSTATE para ODBC 2. *x* y ODBC 3. *x*. Para obtener más información sobre ODBC 3. *x* valores de SQLSTATE, consulte [Apéndice A: códigos de Error de ODBC](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md).  
  
 En ODBC 3. *x*, HYxxx SQLSTATE se devuelven en lugar de S1xxx y 42Sxx SQLSTATE se devuelve en lugar de S00XX. Esto se hacía para alinearse con estándares Open Group e ISO. En muchos casos, la asignación no es uno a uno porque los estándares han redefinido la interpretación de SQLSTATE varias.  
  
 Cuando un ODBC 2. *x* aplicación se actualiza a una aplicación ODBC 3. *x* aplicación, la aplicación tiene que cambiar para esperar que ODBC 3. *x* SQLSTATEs en lugar de ODBC 2. *x* SQLSTATEs. En la tabla siguiente se enumera ODBC 3. *x* SQLSTATE que cada ODBC 2. *x* SQLSTATE se asigna a.  
  
 Cuando se establece el atributo de entorno SQL_ATTR_ODBC_VERSION en SQL_OV_ODBC2, el controlador envía ODBC 2. *x* SQLSTATEs en lugar de ODBC 3. *x* SQLSTATEs cuando **SQLGetDiagField** o **SQLGetDiagRec** se llama. Una asignación determinada se puede determinar mediante la anotación de la API ODBC 2*.x* SQLSTATE en la columna 1 de la siguiente tabla que corresponde a ODBC 3. *x* SQLSTATE en la columna 2.  
  
|ODBC 2. *x* SQLSTATE|ODBC 3. *x* SQLSTATE|Comentarios|  
|-------------------------|-------------------------|--------------|  
|01S03|01001||  
|01S04|01001||  
|22003|HY019||  
|22008|22007||  
|22005|22018||  
|24000|07005||  
|37000|42000||  
|70100|HY018||  
|S0001|42S01||  
|S0002|42S02||  
|S0011|42S11||  
|S0012|42S12||  
|S0021|42S21||  
|S0022|42S22||  
|S0023|42S23||  
|S1000|HY000||  
|S1001|HY001||  
|S1002|07009|ODBC 2. *x* S1002 SQLSTATE se asigna a ODBC 3. *x* SQLSTATE 07009 si la función subyacente se **SQLBindCol**, **SQLColAttribute**, **SQLExtendedFetch**, **SQLFetch** , **SQLFetchScroll**, o **SQLGetData**.|  
|S1003|HY003||  
|S1004|HY004||  
|S1008|HY008||  
|S1009|HY009|Devuelve para un uso no válido de un puntero nulo.|  
|S1009|HY024|Devuelve un valor de atributo no válido.|  
|S1009|HY092|Devuelve para actualizar o eliminar datos mediante una llamada a **SQLSetPos**, o agregar, actualizar o eliminar datos mediante una llamada a **SQLBulkOperations**, cuando la simultaneidad es de solo lectura.|  
|S1010|HY007 HY010|SQLSTATE S1010 se asigna a SQLSTATE HY007 cuando **SQLDescribeCol** se llama antes de llamar a **SQLPrepare**, **SQLExecDirect**, o una función de catálogo para el *StatementHandle*. En caso contrario, se asigna SQLSTATE S1010 a SQLSTATE HY010.|  
|S1011|HY011||  
|S1012|HY012||  
|S1090|HY090||  
|S1091|HY091||  
|S1092|HY092||  
|S1093|07009|ODBC 3. *x* SQLSTATE 07009 se asigna a la API ODBC 2. *x* SQLSTATE S1093 si la función subyacente se **SQLBindParameter** o **SQLDescribeParam**.|  
|S1096|HY096||  
|S1097|HY097||  
|S1098|HY098||  
|S1099|HY099||  
|S1100|HY100||  
|S1101|HY101||  
|S1103|HY103||  
|S1104|HY104||  
|S1105|HY105||  
|S1106|HY106||  
|S1107|HY107||  
|S1108|HY108||  
|S1109|HY109||  
|S1110|HY110||  
|S1111|HY111||  
|S1C00|HYC00||  
|S1T00|HYT00||  
  
> [!NOTE]  
>  ODBC 3. *x* SQLSTATE 07008 se asigna a la API ODBC 2. *x* SQLSTATE S1000.
