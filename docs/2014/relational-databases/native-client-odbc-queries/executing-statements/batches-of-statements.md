---
title: Lotes de instrucciones | Documentos de Microsoft
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
- statements [ODBC], batches
- batches [ODBC]
- ODBC applications, statements
- multiple statements, batches
- SQLMoreResults function
- SQLExecDirect function
ms.assetid: 057d7c1c-1428-4780-9447-a002ea741188
caps.latest.revision: 35
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 2ebe40de44765e974a63fc0eb6282ae0b979b607
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36197919"
---
# <a name="batches-of-statements"></a>Lotes de instrucciones
  Un lote de [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrucciones contiene dos o más instrucciones, separadas por punto y coma (;), integrado en una sola cadena pasada a **SQLExecDirect** o [SQLPrepare Function](http://go.microsoft.com/fwlink/?LinkId=59360). Por ejemplo:  
  
```  
SQLExecDirect(hstmt,   
    "SELECT * FROM Authors; SELECT * FROM Titles",  
    SQL_NTS);  
```  
  
 Los lotes pueden ser más eficaces que el envío de instrucciones por separado porque el tráfico de red suele ser reducido. Use [SQLMoreResults](../../native-client-odbc-api/sqlmoreresults.md) para situarse en el siguiente conjunto de resultados cuando termine con el conjunto de resultados actual.  
  
 Siempre pueden usarse lotes cuando los atributos de cursor de ODBC se establecen en los valores predeterminados de un cursor de solo avance y de solo lectura cuyo conjunto de filas tiene un tamaño de 1.  
  
 Si se ejecuta un lote al utilizar los cursores del servidor en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], el cursor del servidor se convierte implícitamente en un conjunto de resultados predeterminado. **SQLExecDirect** o **SQLExecute** devuelve SQL_SUCCESS_WITH_INFO y una llamada a **SQLGetDiagRec** devuelve:  
  
```  
szSqlState = "01S02", pfNativeError = 0  
szErrorMsg = "[Microsoft][SQL Server Native Server Native Client]Cursor type changed."  
```  
  
## <a name="see-also"></a>Vea también  
 [Ejecutar instrucciones &#40;ODBC&#41;](executing-statements-odbc.md)  
  
  