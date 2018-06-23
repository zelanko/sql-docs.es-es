---
title: Conversiones de Cursor implícitas (ODBC) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ODBC cursors, implicit cursor conversions
- implicit cursor conversions
- cursors [ODBC], implicit cursor conversions
ms.assetid: fe29a58d-8448-4512-9ffd-b414784ba338
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b1f1880ea464949bd962bab002d1f1129261463c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36110925"
---
# <a name="implicit-cursor-conversions-odbc"></a>Conversiones de cursor implícitas (ODBC)
  Las aplicaciones pueden solicitar un tipo de cursor a través de [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) y, a continuación, ejecutar una instrucción SQL que no es compatible con los cursores de servidor del tipo solicitado. Una llamada a **SQLExecute** o **SQLExecDirect** devuelve SQL_SUCCESS_WITH_INFO y **SQLGetDiagRec** devuelve:  
  
```  
szSqlState = "01S02", *pfNativeError = 0,  
szErrorMsg="[Microsoft][SQL Server Native Client] Cursor type changed"  
```  
  
 La aplicación puede determinar qué tipo de cursor ahora está usándola mediante una llamada a **SQLGetStmtOption** establecido en SQL_CURSOR_TYPE. La conversión del tipo de cursor solamente se aplica a una instrucción. La siguiente **SQLExecDirect** o **SQLExecute** se hará mediante la configuración original de cursor de instrucción.  
  
## <a name="see-also"></a>Vea también  
 [Detalles de la programación de cursor &#40;ODBC&#41;](cursor-programming-details-odbc.md)  
  
  