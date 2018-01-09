---
title: Usar conjuntos de resultados predeterminados SQL Server | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-cursors
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQLSetStmtAttr function
- ODBC cursors, default result sets
- cursors [ODBC], default result sets
- default result sets
- result sets [ODBC], default
- ODBC applications, cursors
ms.assetid: ee1db3e5-60eb-4425-8a6b-977eeced3f98
caps.latest.revision: "36"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 165ab316554f8a42cae5f08e858b73d14298c265
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="using-sql-server-default-result-sets"></a>Utilizar conjuntos de resultados predeterminados de SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Los atributos de cursor ODBC predeterminados son:  
  
```  
SQLSetStmtAttr(hstmt, SQL_ATTR_CURSOR_TYPE, SQL_CURSOR_FORWARD_ONLY, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_CONCURRENCY, SQL_CONCUR_READ_ONLY, SQL_IS_INTEGER);  
SQLSetStmtAttr(hstmt, SQL_ATTR_ROW_ARRAY_SIZE, 1, SQL_IS_INTEGER);  
```  
  
 Siempre que estos atributos se establecen en sus valores predeterminados, el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client utiliza un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] conjunto de resultados predeterminado. Los conjuntos de resultados predeterminados se pueden utilizar para cualquier instrucción SQL admitida por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y son el método más eficaz de transferir un conjunto de resultados completo al cliente.  
  
 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]incorpora compatibilidad con de conjuntos de resultados activos múltiples (MARS); las aplicaciones ahora pueden tener más de un conjunto de resultados predeterminado activo por conexión. MARS no está habilitado de forma predeterminada.  
  
 Antes de [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], los conjuntos de resultados predeterminados no admitían varias instrucciones activas en la misma conexión. Una vez ejecutada una instrucción SQL en una conexión, el servidor no acepta comandos (excepto una solicitud para cancelar el resto del conjunto de resultados) del cliente en esa conexión hasta que se han procesado todas las filas del conjunto de resultados. Para cancelar el resto de un conjunto de resultados procesado parcialmente, llame a [SQLCloseCursor](../../../relational-databases/native-client-odbc-api/sqlclosecursor.md) o [SQLFreeStmt](../../../relational-databases/native-client-odbc-api/sqlfreestmt.md) con el *fOption* parámetro establecido en SQL_CLOSE. Para finalizar un conjunto de resultados procesado parcialmente y comprobar la presencia de otro conjunto de resultados, llame a [SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md). Si una aplicación ODBC intenta ejecutar un comando en un identificador de conexión antes de que se ha procesado completamente el conjunto de resultados predeterminado, la llamada genera SQL_ERROR y una llamada a **SQLGetDiagRec** devuelve:  
  
```  
szSqlState: "HY000", pfNativeError: 0  
szErrorMsg: "[Microsoft][SQL Server Native Client]  
                Connection is busy with results for another hstmt."  
```  
  
## <a name="see-also"></a>Vea también  
 [Cómo se implementan los cursores](../../../relational-databases/native-client-odbc-cursors/implementation/how-cursors-are-implemented.md)  
  
  
