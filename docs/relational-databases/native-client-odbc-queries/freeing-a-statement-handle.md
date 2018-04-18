---
title: Liberar un identificador de instrucción | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-queries
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- reusing statement handles
- freeing statement handles
- statements [ODBC], statement handles
- SQLFreeStmt function
- ODBC applications, statements
- statement handles [ODBC]
ms.assetid: 96fdff84-0ca7-460a-a240-94ee826ea41c
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1c260f86fd5fa828cedd02a55e2f020333696f39
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="freeing-a-statement-handle"></a>Liberar un identificador de instrucción
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Es más eficaz volver a utilizar los identificadores de instrucciones que quitarlos y asignar unos nuevos. Antes de ejecutar una nueva instrucción SQL en un identificador de instrucciones, las aplicaciones deberían comprobar que la configuración de instrucción actual es correcta. Éstos incluyen atributos de instrucción, enlaces de parámetros y enlaces de conjunto de resultados. Por lo general, parámetros y conjuntos de resultados de la instrucción SQL anterior debe ser no enlazada mediante una llamada a [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) con el SQL_RESET_PARAMS y SQL_UNBIND opciones y, a continuación, volver a enlazar la nueva instrucción SQL.  
  
 Cuando la aplicación ha terminado de usar la instrucción, llama al método [SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) para liberar la instrucción. Tenga en cuenta que **SQLDisconnect** libera automáticamente todas las instrucciones de una conexión.  
  
## <a name="see-also"></a>Vea también  
 [Ejecutar consultas &#40;ODBC&#41;](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
