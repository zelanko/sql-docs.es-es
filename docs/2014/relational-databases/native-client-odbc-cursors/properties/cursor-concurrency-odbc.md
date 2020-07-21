---
title: Simultaneidad de cursores (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- concurrency [ODBC]
- cursors [ODBC], concurrency
- ODBC cursors, concurrency
ms.assetid: 68228ece-cbf1-4f19-bfdc-053884c1af48
author: rothja
ms.author: jroth
ms.openlocfilehash: c47f24152978fedf8f2c3d49ec3b721969712814
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85020590"
---
# <a name="cursor-concurrency-odbc"></a>Simultaneidad de cursor (ODBC)
  Las opciones de simultaneidad establecidas por la aplicación afectan a las operaciones del cursor, como los tipos de cursor. Las opciones de simultaneidad se establecen mediante la opción SQL_ATTR_CONCURRENCY de [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md). Los tipos de simultaneidad son:  
  
-   Solo lectura (SQL_CONCUR_READONLY)  
  
-   Valores (SQL_CONCUR_VALUES)  
  
-   Versión de fila (SQL_CONCUR_ROWVER)  
  
-   Bloqueo (SQL_CONCUR_LOCK)  
  
## <a name="see-also"></a>Consulte también  
 [Propiedades de cursor](cursor-properties.md)  
  
  
