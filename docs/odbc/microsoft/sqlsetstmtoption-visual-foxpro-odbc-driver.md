---
title: SQLSetStmtOption (Controlador ODBC de Visual FoxPro) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetStmtOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 76b813e3-c7dc-4bb2-a710-d2aa9dcfdc36
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cb9677a9ccf307be847089c657964d96904eb20b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299405"
---
# <a name="sqlsetstmtoption-visual-foxpro-odbc-driver"></a>SQLSetStmtOption (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general sobre esta función, consulte el tema adecuado en Referencia de [la API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte: Completo  
  
 Conformidad de la API ODBC: Nivel 1  
  
 Establece las opciones relacionadas con un identificador de instrucción, *hstmt*.  
  
|*fOption*|Valores permitidos|Comentarios|  
|---------------|--------------------|--------------|  
|SQL_ASYNC_ENABLE|SQL_ASYNC_ENABLE_OFF|Si intenta establecer este *fOption*, el controlador devuelve el error: "Driver not capable". Visual FoxPro no admite la ejecución asincrónica.|  
|SQL_BIND_TYPE|SQL_BIND_BY_COLUMN o un valor de 32 bits que indica la longitud de la estructura o una instancia de un búfer en el que se enlazarán las columnas de resultados.||  
|SQL_CONCURRENCY|SQL_CONCUR_READ_ONLY<br /><br /> SQL_CONCUR_LOCK<br /><br /> SQL_CONCUR_VALUES|El controlador no permite SQL_CONCUR_ROWVER, porque Visual FoxPro no tiene control de versiones de fila basado en marcas de tiempo.|  
|SQL_CURSOR_TYPE|SQL_CURSOR_FORWARD_ONLY<br /><br /> SQL_CURSOR_STATIC|El controlador no permite SQL_CURSOR_KEYSET_DRIVEN o SQL_CURSOR_DYNAMIC; consulte [SQLSetScrollOptions](../../odbc/microsoft/sqlsetscrolloptions-visual-foxpro-odbc-driver.md) para obtener más información.|  
|SQL_KEYSET_SIZE|Error: "Driver not capable"|Visual FoxPro no admite el modelo de cursor de conjunto de claves.|  
|SQL_MAX_LENGTH|0|Si intenta establecer este valor *fOption,* el controlador devuelve el error "Driver not capable".|  
|SQL_MAX_ROWS|0|Si intenta establecer este valor *fOption,* el controlador devuelve el error "Driver not capable".|  
|SQL_NOSCAN|SQL_NOSCAN_OFF||  
|SQL_QUERY_TIMEOUT|0|Si intenta establecer este valor *fOption,* el controlador devuelve el error "Driver not capable".|  
|SQL_RETRIEVE_DATA|SQL_RD_ON, SQL_RD_OFF||  
|SQL_ROWSET_SIZE|1 a 4.294.967.296||  
|SQL_SIMULATE_CURSOR|Error: "Driver not capable"||  
|SQL_USE_BOOKMARKS|SQL_UB_OFF<br /><br /> SQL_UB_ON||  
  
 Para obtener más información, vea [SQLSetStmtOption](../../odbc/reference/syntax/sqlsetstmtoption-function.md) en la *referencia del programador ODBC*.
