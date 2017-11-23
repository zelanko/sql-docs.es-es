---
title: "Liberar un identificador de instrucción | Documentos de Microsoft"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-queries
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- reusing statement handles
- freeing statement handles
- statements [ODBC], statement handles
- SQLFreeStmt function
- ODBC applications, statements
- statement handles [ODBC]
ms.assetid: 96fdff84-0ca7-460a-a240-94ee826ea41c
caps.latest.revision: "32"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3c1d18006b85b8017600504b02ed9b557b34befa
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="freeing-a-statement-handle"></a>Liberar un identificador de instrucción
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Es más eficaz volver a utilizar los identificadores de instrucciones que quitarlos y asignar unos nuevos. Antes de ejecutar una nueva instrucción SQL en un identificador de instrucciones, las aplicaciones deberían comprobar que la configuración de instrucción actual es correcta. Éstos incluyen atributos de instrucción, enlaces de parámetros y enlaces de conjunto de resultados. Por lo general, parámetros y conjuntos de resultados de la instrucción SQL anterior debe ser no enlazada mediante una llamada a [SQLFreeStmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) con el SQL_RESET_PARAMS y SQL_UNBIND opciones y, a continuación, volver a enlazar la nueva instrucción SQL.  
  
 Cuando la aplicación ha terminado de usar la instrucción, llama al método [SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) para liberar la instrucción. Tenga en cuenta que **SQLDisconnect** libera automáticamente todas las instrucciones de una conexión.  
  
## <a name="see-also"></a>Vea también  
 [Ejecución de consultas &#40; ODBC &#41;](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
