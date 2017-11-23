---
title: Compatibilidad con transacciones en DBMS | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 0fc2ae34-4748-4120-9fc3-bb28c8ed867e
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5785d2df5e9b1a3dccef92b8cf3e7996e88e6056
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="transaction-support-in-dbmss"></a>Compatibilidad con transacciones en DBMS
Algunas bases de datos, especialmente escritorio bases de datos, como dBASE y Paradox, Btrieve, no son compatibles con las transacciones. Incluso entre las bases de datos que admiten transacciones, hay variación en qué tipos de instrucciones SQL que pueden estar en una transacción. Para obtener más información, vea la opción SQL_TXN_CAPABLE en la [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descripción de la función.
