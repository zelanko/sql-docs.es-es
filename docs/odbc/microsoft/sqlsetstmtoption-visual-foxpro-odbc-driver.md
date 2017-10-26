---
title: SQLSetStmtOption (controlador ODBC de Visual FoxPro) | Documentos de Microsoft
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
- SQLSetStmtOption function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 76b813e3-c7dc-4bb2-a710-d2aa9dcfdc36
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 9374aed937aed17c0e1157eb6523f9b313473698
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetstmtoption-visual-foxpro-odbc-driver"></a>SQLSetStmtOption (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte técnico: completo  
  
 Ajuste de la API de ODBC: Nivel 1  
  
 Establece opciones relacionadas con un identificador de instrucción, *hstmt*.  
  
|*fOption*|Valores permitidos|Comentarios|  
|---------------|--------------------|--------------|  
|SQL_ASYNC_ENABLE|SQL_ASYNC_ENABLE_OFF|Si se intenta establecer esto *fOption*, el controlador devuelve el error: "No compatible con el controlador". Visual FoxPro no admite la ejecución asincrónica.|  
|SQL_BIND_TYPE|SQL_BIND_BY_COLUMN o un valor de 32 bits que indica la longitud de la estructura o una instancia de un búfer en qué resultado se enlazarán las columnas.||  
|SQL_CONCURRENCY|SQL_CONCUR_READ_ONLY<br /><br /> SQL_CONCUR_LOCK<br /><br /> SQL_CONCUR_VALUES|El controlador no permite SQL_CONCUR_ROWVER, porque Visual FoxPro no tiene las versiones de fila en función de las marcas de tiempo.|  
|SQL_CURSOR_TYPE|SQL_CURSOR_FORWARD_ONLY<br /><br /> SQL_CURSOR_STATIC|El controlador no permite SQL_CURSOR_KEYSET_DRIVEN o SQL_CURSOR_DYNAMIC; vea [SQLSetScrollOptions](../../odbc/microsoft/sqlsetscrolloptions-visual-foxpro-odbc-driver.md) para obtener más información.|  
|SQL_KEYSET_SIZE|Error: "el controlador no capaz."|Visual FoxPro no admite el modelo de cursor de conjunto de claves.|  
|SQL_MAX_LENGTH|0|Si se intenta establecer esto *fOption* valor, el controlador devuelve el error "No compatible con el controlador".|  
|SQL_MAX_ROWS|0|Si se intenta establecer esto *fOption* valor, el controlador devuelve el error "No compatible con el controlador".|  
|SQL_NOSCAN|SQL_NOSCAN_OFF||  
|SQL_QUERY_TIMEOUT|0|Si se intenta establecer esto *fOption* valor, el controlador devuelve el error "No compatible con el controlador".|  
|SQL_RETRIEVE_DATA|SQL_RD_ON, SQL_RD_OFF||  
|SQL_ROWSET_SIZE|1 a 4.294.967.296||  
|SQL_SIMULATE_CURSOR|Error: "el controlador no capaz."||  
|SQL_USE_BOOKMARKS|SQL_UB_OFF<br /><br /> SQL_UB_ON||  
  
 Para obtener más información, consulte [SQLSetStmtOption](../../odbc/reference/syntax/sqlsetstmtoption-function.md) en el *referencia del programador de ODBC*.

