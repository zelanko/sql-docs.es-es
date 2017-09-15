---
title: Compatibilidad con transacciones en DBMS | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 0fc2ae34-4748-4120-9fc3-bb28c8ed867e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 14c1519122484542b57e286c248c25c3fd6c0886
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="transaction-support-in-dbmss"></a>Compatibilidad con transacciones en DBMS
Algunas bases de datos, especialmente escritorio bases de datos, como dBASE y Paradox, Btrieve, no son compatibles con las transacciones. Incluso entre las bases de datos que admiten transacciones, hay variación en qué tipos de instrucciones SQL que pueden estar en una transacción. Para obtener más información, vea la opción SQL_TXN_CAPABLE en la [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descripción de la función.
