---
title: SQLSetStmtOption (controlador ODBC de Visual FoxPro) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a026922cb98fdb520c9eeab223c8b34a231a179e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67905332"
---
# <a name="sqlsetstmtoption-visual-foxpro-odbc-driver"></a>SQLSetStmtOption (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general sobre esta función, vea el tema correspondiente en referencia de la [API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Compatibilidad: completa  
  
 Conformidad con la API de ODBC: nivel 1  
  
 Establece las opciones relacionadas con un identificador de instrucción, *hstmt*.  
  
|*fOption*|Valores permitidos|Comentarios|  
|---------------|--------------------|--------------|  
|SQL_ASYNC_ENABLE|SQL_ASYNC_ENABLE_OFF|Si intenta establecer este *fOption*, el controlador devolverá el error: "controlador no compatible". Visual FoxPro no admite la ejecución asincrónica.|  
|SQL_BIND_TYPE|SQL_BIND_BY_COLUMN o un valor de 32 bits que denota la longitud de la estructura o una instancia de un búfer en el que se enlazarán las columnas de resultados.||  
|SQL_CONCURRENCY|SQL_CONCUR_READ_ONLY<br /><br /> SQL_CONCUR_LOCK<br /><br /> SQL_CONCUR_VALUES|El controlador no permite SQL_CONCUR_ROWVER, porque Visual FoxPro no tiene versiones de fila basadas en marcas de tiempo.|  
|SQL_CURSOR_TYPE|SQL_CURSOR_FORWARD_ONLY<br /><br /> SQL_CURSOR_STATIC|El controlador no permite SQL_CURSOR_KEYSET_DRIVEN o SQL_CURSOR_DYNAMIC; vea [SQLSetScrollOptions](../../odbc/microsoft/sqlsetscrolloptions-visual-foxpro-odbc-driver.md) para obtener más información.|  
|SQL_KEYSET_SIZE|Error: "controlador no compatible"|Visual FoxPro no admite el modelo de cursor de conjunto de claves.|  
|SQL_MAX_LENGTH|0|Si intenta establecer este valor de *fOption* , el controlador devuelve el error "controlador no compatible".|  
|SQL_MAX_ROWS|0|Si intenta establecer este valor de *fOption* , el controlador devuelve el error "controlador no compatible".|  
|SQL_NOSCAN|SQL_NOSCAN_OFF||  
|SQL_QUERY_TIMEOUT|0|Si intenta establecer este valor de *fOption* , el controlador devuelve el error "controlador no compatible".|  
|SQL_RETRIEVE_DATA|SQL_RD_ON, SQL_RD_OFF||  
|SQL_ROWSET_SIZE|de 1 a 4.294.967.296||  
|SQL_SIMULATE_CURSOR|Error: "controlador no compatible"||  
|SQL_USE_BOOKMARKS|SQL_UB_OFF<br /><br /> SQL_UB_ON||  
  
 Para obtener más información, vea [SQLSetStmtOption](../../odbc/reference/syntax/sqlsetstmtoption-function.md) en la *Referencia del programador de ODBC*.
