---
description: Simultaneidad de cursor (ODBC)
title: Simultaneidad de cursores (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- concurrency [ODBC]
- cursors [ODBC], concurrency
- ODBC cursors, concurrency
ms.assetid: 68228ece-cbf1-4f19-bfdc-053884c1af48
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 343eaeceeb12e71f0df9b4a2791120007effac46
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97473726"
---
# <a name="cursor-concurrency-odbc"></a>Simultaneidad de cursor (ODBC)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Las opciones de simultaneidad establecidas por la aplicación afectan a las operaciones del cursor, como los tipos de cursor. Las opciones de simultaneidad se establecen mediante la opción SQL_ATTR_CONCURRENCY de [SQLSetStmtAttr](../../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md). Los tipos de simultaneidad son:  
  
-   Solo lectura (SQL_CONCUR_READONLY)  
  
-   Valores (SQL_CONCUR_VALUES)  
  
-   Versión de fila (SQL_CONCUR_ROWVER)  
  
-   Bloqueo (SQL_CONCUR_LOCK)  
  
## <a name="see-also"></a>Consulte también  
 [Propiedades de cursor](../../../relational-databases/native-client-odbc-cursors/properties/cursor-properties.md)  
  
  
