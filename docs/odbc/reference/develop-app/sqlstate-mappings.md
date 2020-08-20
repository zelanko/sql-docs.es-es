---
description: Asignaciones SQLSTATE
title: Asignaciones de SQLSTATE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLSTATE
- backward compatibility [ODBC], SQLSTATE
- SQLSTATE [ODBC]
ms.assetid: 6e6cabcf-a204-40eb-b77d-8a0c4a5e8524
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 14be1946b34433b0ff094cb79e2a1ec2ee849cd3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476407"
---
# <a name="sqlstate-mappings"></a>Asignaciones SQLSTATE
En este tema se describen los valores de SQLSTATE para ODBC *2. x* y ODBC *3. x*. Para obtener más información sobre los valores de SQLSTATE de ODBC *3. x* , vea [el Apéndice A: códigos de error ODBC](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md).  
  
 En ODBC *3. x*, se devuelven HYxxx SQLSTATEs en lugar de S1xxx y se devuelven 42Sxx SQLSTATEs en lugar de S00XX. Esto se hizo para ajustarse a los estándares de grupo abierto e ISO. En muchos casos, la asignación no es de uno a uno porque los estándares han redefinido la interpretación de varios SQLSTATEs.  
  
 Cuando una aplicación ODBC *2. x* se actualiza a una aplicación ODBC *3. x* , se debe cambiar la aplicación para que se espere el SQLSTATEs ODBC *3. x* en lugar de ODBC *2. x* SQLSTATEs. En la tabla siguiente se enumeran los SQLSTATEs de ODBC *3. x* a los que se asigna cada SQLSTATE ODBC *2. x* .  
  
 Cuando el atributo de entorno SQL_ATTR_ODBC_VERSION está establecido en SQL_OV_ODBC2, el controlador expone ODBC *2. x* SQLSTATEs en lugar de ODBC *3. x* SQLSTATEs cuando se llama a **SQLGetDiagField** o **SQLGetDiagRec** . Se puede determinar una asignación específica indicando el SQLSTATE ODBC *2. x* de la columna 1 de la tabla siguiente, que corresponde al SQLSTATE ODBC *3. x* de la columna 2.  
  
|ODBC *2. x* SQLSTATE|ODBC *3. x* SQLSTATE|Comentarios|  
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
|S1002|07009|ODBC *2. x* SQLSTATE S1002 se asigna a ODBC *3. x* SQLSTATE 07009 si la función subyacente es **SQLBindCol**, **SQLColAttribute**, **SQLExtendedFetch**, **SQLFetch**, **SQLFetchScroll**o **SQLGetData**.|  
|S1003|HY003||  
|S1004|HY004||  
|S1008|HY008||  
|S1009|HY009|Se devuelve para un uso no válido de un puntero NULL.|  
|S1009|HY024|Se devuelve para un valor de atributo no válido.|  
|S1009|HY092|Se devuelve para actualizar o eliminar los datos mediante una llamada a **SQLSetPos**, o para agregar, actualizar o eliminar datos mediante una llamada a **SQLBulkOperations**, cuando la simultaneidad es de solo lectura.|  
|S1010|HY007 HY010|SQLSTATE S1010 se asigna a SQLSTATE HY007 cuando se llama a **SQLDescribeCol** antes de llamar a **SQLPrepare**, **SQLExecDirect**o a una función de catálogo para *StatementHandle*. De lo contrario, SQLSTATE S1010 se asigna a SQLSTATE HY010.|  
|S1011|HY011||  
|S1012|HY012||  
|S1090|HY090||  
|S1091|HY091||  
|S1092|HY092||  
|S1093|07009|ODBC *3. x* SQLSTATE 07009 está asignado a ODBC *2. x* SQLSTATE S1093 si la función subyacente es **SQLBindParameter** o **SQLDescribeParam**.|  
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
>  ODBC *3. x* SQLSTATE 07008 está asignado a ODBC *2. x* SQLSTATE S1000.
