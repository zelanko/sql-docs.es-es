---
title: Usar SQL Server conjuntos de resultados predeterminados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQLSetStmtAttr function
- ODBC cursors, default result sets
- cursors [ODBC], default result sets
- default result sets
- result sets [ODBC], default
- ODBC applications, cursors
ms.assetid: ee1db3e5-60eb-4425-8a6b-977eeced3f98
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1d7101cf4775e5280c22cc27ecae009410d231d5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/25/2020
ms.locfileid: "62511690"
---
# <a name="using-sql-server-default-result-sets"></a>Utilizar conjuntos de resultados predeterminados de SQL Server
  Los atributos de cursor ODBC predeterminados son:  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_FORWARD_ONLY, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_CONCURRENCY, SQL_CONCUR_READ_ONLY, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, 1, SQL_IS_INTEGER);  
```  
  
 Cada vez que estos atributos se establecen en sus valores predeterminados, el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de Native Client utiliza un conjunto de resultados predeterminado. Los conjuntos de resultados predeterminados se pueden utilizar para cualquier instrucción SQL admitida por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y son el método más eficaz de transferir un conjunto de resultados completo al cliente.  
  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]se incorporó la compatibilidad con conjuntos de resultados activos múltiples (MARS). Ahora, las aplicaciones pueden tener más de un conjunto de resultados predeterminado activo por conexión. MARS no está habilitado de forma predeterminada.  
  
 Antes de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], los conjuntos de resultados predeterminados no admitían varias instrucciones activas en la misma conexión. Una vez ejecutada una instrucción SQL en una conexión, el servidor no acepta comandos (excepto una solicitud para cancelar el resto del conjunto de resultados) del cliente en esa conexión hasta que se han procesado todas las filas del conjunto de resultados. Para cancelar el resto de un conjunto de resultados procesado parcialmente, llame a [SQLCloseCursor](../../native-client-odbc-api/sqlclosecursor.md) o [SQLFreeStmt](../../native-client-odbc-api/sqlfreestmt.md) con el parámetro *fOption* establecido en SQL_CLOSE. Para finalizar un conjunto de resultados procesado parcialmente y probar la presencia de otro conjunto de resultados, llame a [SQLMoreResults](../../native-client-odbc-api/sqlmoreresults.md). Si una aplicación ODBC intenta un comando en un identificador de conexión antes de que se haya procesado completamente un conjunto de resultados predeterminado, la llamada genera SQL_ERROR y una llamada a **SQLGetDiagRec** devuelve:  
  
```  
szSqlState: "HY000", pfNativeError: 0  
szErrorMsg: "[Microsoft][SQL Server Native Client]  
                Connection is busy with results for another hstmt."  
```  
  
## <a name="see-also"></a>Consulte también  
 [Cómo se implementan los cursores](how-cursors-are-implemented.md)  
  
  
