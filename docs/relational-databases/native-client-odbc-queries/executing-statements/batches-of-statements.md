---
title: Lotes de instrucciones | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 54015c65dbaff5a30148dcc29d2095df47c9bc80
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39563449"
---
# <a name="batches-of-statements"></a>Lotes de instrucciones
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Un lote de [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrucciones contiene dos o más instrucciones, separadas por punto y coma (;), integrado en una sola cadena pasada a **SQLExecDirect** o [SQLPrepare Function](http://go.microsoft.com/fwlink/?LinkId=59360). Por ejemplo:  
  
```  
SQLExecDirect(hstmt,   
    "SELECT * FROM Authors; SELECT * FROM Titles",  
    SQL_NTS);  
```  
  
 Los lotes pueden ser más eficaces que el envío de instrucciones por separado porque el tráfico de red suele ser reducido. Use [SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md) para situarse en el siguiente conjunto de resultados cuando termine con el conjunto de resultados actual.  
  
 Siempre pueden usarse lotes cuando los atributos de cursor de ODBC se establecen en los valores predeterminados de un cursor de solo avance y de solo lectura cuyo conjunto de filas tiene un tamaño de 1.  
  
 Si se ejecuta un lote al utilizar los cursores del servidor en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], el cursor del servidor se convierte implícitamente en un conjunto de resultados predeterminado. **SQLExecDirect** o **SQLExecute** devuelve SQL_SUCCESS_WITH_INFO y una llamada a **SQLGetDiagRec** devuelve:  
  
```  
szSqlState = "01S02", pfNativeError = 0  
szErrorMsg = "[Microsoft][SQL Server Native Server Native Client]Cursor type changed."  
```  
  
## <a name="see-also"></a>Vea también  
 [Ejecución de instrucciones &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
