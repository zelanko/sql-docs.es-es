---
title: Compatibilidad con transacciones en DBMS | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2fed5ea04e15002d31e35e25fac405a729929be8
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47692273"
---
# <a name="transaction-support-in-dbmss"></a>Compatibilidad con transacciones en DBMS
Algunas bases de datos, especialmente escritorio bases de datos de dBASE, Paradox y Btrieve, no admiten transacciones. Incluso entre las bases de datos que admiten transacciones, hay variación en lo que pueden ser tipos de instrucciones SQL en una transacción. Para obtener más información, vea la opción SQL_TXN_CAPABLE en el [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descripción de la función.
