---
description: Compatibilidad con transacciones
title: Compatibilidad con transacciones | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transactions [ODBC], degree of support
ms.assetid: d56e1458-8da2-4d73-a777-09e045c30a33
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0218941606752ccd93c7bc9bdfe31096682c6d87
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476334"
---
# <a name="transaction-support"></a>Compatibilidad con transacciones
El grado de compatibilidad con transacciones está definido por el controlador. ODBC está diseñado para implementarse en una base de datos de un solo usuario o de escritorio que no tiene necesidad de administrar varias actualizaciones de sus datos. Además, algunas bases de datos que admiten transacciones solo lo hacen para las instrucciones del lenguaje de manipulación de datos (DML) de SQL. Existen restricciones o semántica de transacciones especiales con respecto al uso del lenguaje de definición de datos (DDL) cuando una transacción está activa. Es decir, puede haber compatibilidad con transacciones para varias actualizaciones simultáneas en tablas, pero no para cambiar el número y la definición de tablas durante una transacción.  
  
 Una aplicación determina si se admiten las transacciones, si se puede incluir DDL en una transacción y los efectos especiales de incluir DDL en una transacción, llamando a **SQLGetInfo** con la opción SQL_TXN_CAPABLE. Para obtener más información, vea la descripción de la función [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) .  
  
 Si el controlador no admite transacciones pero la aplicación tiene la capacidad (mediante una API distinta de ODBC) para bloquear y desbloquear datos, las aplicaciones pueden lograr la compatibilidad con transacciones bloqueando y desbloqueando los registros y las tablas según sea necesario. Para implementar el ejemplo de transferencia de cuenta, la aplicación bloquearía los registros de ambas cuentas, copiará los valores actuales, adeudará la primera cuenta, abonará la segunda cuenta y desbloqueará los registros. Si se produce un error en alguno de los pasos, la aplicación restablecería las cuentas mediante las copias.  
  
 Incluso los orígenes de datos que admiten transacciones podrían no ser capaces de admitir más de una transacción a la vez dentro de un entorno determinado. Las aplicaciones llaman a **SQLGetInfo** con la opción SQL_MULTIPLE_ACTIVE_TXN para determinar si un origen de datos puede admitir transacciones activas simultáneas en más de una conexión en el mismo entorno. Dado que hay una transacción por conexión, esto solo es interesante para las aplicaciones que tienen varias conexiones con el mismo origen de datos.
