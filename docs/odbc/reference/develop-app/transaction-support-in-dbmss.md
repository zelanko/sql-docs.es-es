---
title: Soporte de transacciones en DBMSs ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 0fc2ae34-4748-4120-9fc3-bb28c8ed867e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b6da6fdc819d8852aadcd7b672ef06e99d46c0ea
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298010"
---
# <a name="transaction-support-in-dbmss"></a>Compatibilidad con transacciones en DBMS
Algunas bases de datos, especialmente las bases de datos de escritorio como dBASE, Paradox y Btrieve, no admiten transacciones. Incluso entre las bases de datos que admiten transacciones, hay variación en qué tipos de instrucciones SQL pueden estar en una transacción. Para obtener más información, vea la opción SQL_TXN_CAPABLE en la descripción de la función [SQLGetInfo.](../../../odbc/reference/syntax/sqlgetinfo-function.md)
