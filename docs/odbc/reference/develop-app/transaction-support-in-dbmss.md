---
description: Compatibilidad con transacciones en DBMS
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b8e0b3433e0f666af100cce5e72e36b685533b1d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487458"
---
# <a name="transaction-support-in-dbmss"></a>Compatibilidad con transacciones en DBMS
Algunas bases de datos, especialmente las bases de datos de escritorio, como dBASE, Paradox y Btrieve, no admiten transacciones. Incluso entre las bases de datos que admiten transacciones, hay una variación en la que los tipos de instrucciones SQL pueden estar en una transacción. Para obtener más información, vea la opción SQL_TXN_CAPABLE en la descripción de la función [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) .
