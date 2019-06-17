---
title: SQLSetStmtOption (Visual FoxPro ODBC Driver) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 9d7bcecfbd880f53d1067fd68202b62c34fce398
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63305818"
---
# <a name="sqlsetstmtoption-visual-foxpro-odbc-driver"></a>SQLSetStmtOption (controlador ODBC de Visual FoxPro)
> [!NOTE]  
>  Este tema contiene información específica del controlador ODBC de Visual FoxPro. Para obtener información general acerca de esta función, vea el tema correspondiente en [referencia de la API de ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Soporte técnico: Completo  
  
 Conformidad de la API de ODBC: Nivel 1  
  
 Establece las opciones relacionadas con un identificador de instrucción, *hstmt*.  
  
|*fOption*|Valores permitidos|Comentarios|  
|---------------|--------------------|--------------|  
|SQL_ASYNC_ENABLE|SQL_ASYNC_ENABLE_OFF|Si se intenta establecerlo *fOption*, el controlador devuelve el error: "El controlador no compatible con". Visual FoxPro no admite la ejecución asincrónica.|  
|SQL_BIND_TYPE|SQL_BIND_BY_COLUMN o un valor de 32 bits que indica la longitud de la estructura o una instancia de un búfer en el que el resultado se enlazará columnas.||  
|SQL_CONCURRENCY|SQL_CONCUR_READ_ONLY<br /><br /> SQL_CONCUR_LOCK<br /><br /> SQL_CONCUR_VALUES|El controlador no permite SQL_CONCUR_ROWVER, porque Visual FoxPro no tiene las versiones de fila en función de las marcas de tiempo.|  
|SQL_CURSOR_TYPE|SQL_CURSOR_FORWARD_ONLY<br /><br /> SQL_CURSOR_STATIC|El controlador no permite SQL_CURSOR_KEYSET_DRIVEN o SQL_CURSOR_DYNAMIC; consulte [SQLSetScrollOptions](../../odbc/microsoft/sqlsetscrolloptions-visual-foxpro-odbc-driver.md) para obtener más información.|  
|SQL_KEYSET_SIZE|Error: "No compatible con el controlador"|Visual FoxPro no es compatible con el modelo de cursor keyset.|  
|SQL_MAX_LENGTH|0|Si se intenta establecerlo *fOption* valor, el controlador devuelve el error "No compatible con el controlador".|  
|SQL_MAX_ROWS|0|Si se intenta establecerlo *fOption* valor, el controlador devuelve el error "No compatible con el controlador".|  
|SQL_NOSCAN|SQL_NOSCAN_OFF||  
|SQL_QUERY_TIMEOUT|0|Si se intenta establecerlo *fOption* valor, el controlador devuelve el error "No compatible con el controlador".|  
|SQL_RETRIEVE_DATA|SQL_RD_ON, SQL_RD_OFF||  
|SQL_ROWSET_SIZE|1 a 4.294.967.296||  
|SQL_SIMULATE_CURSOR|Error: "No compatible con el controlador"||  
|SQL_USE_BOOKMARKS|SQL_UB_OFF<br /><br /> SQL_UB_ON||  
  
 Para obtener más información, consulte [SQLSetStmtOption](../../odbc/reference/syntax/sqlsetstmtoption-function.md) en el *referencia del programador de ODBC*.
