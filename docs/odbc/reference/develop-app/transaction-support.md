---
title: Soporte de transacciones ? Microsoft Docs
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
ms.openlocfilehash: a5b9d731d12329a4ef663b1ea66cdc59a0b153fa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297983"
---
# <a name="transaction-support"></a>Compatibilidad con transacciones
El grado de soporte para las transacciones está definido por el controlador. ODBC está diseñado para implementarse en una base de datos de un solo usuario o escritorio que no tiene necesidad de administrar varias actualizaciones de sus datos. Además, algunas bases de datos que admiten transacciones solo lo hacen para las instrucciones de lenguaje de manipulación de datos (DML) de SQL; hay restricciones o semántica de transacciones especiales con respecto al uso del lenguaje de definición de datos (DDL) cuando una transacción está activa. Es decir, puede haber compatibilidad con transacciones para varias actualizaciones simultáneas en tablas, pero no para cambiar el número y la definición de tablas durante una transacción.  
  
 Una aplicación determina si se admiten transacciones, si DDL se puede incluir en una transacción y cualquier efecto especial de incluir DDL en una transacción, llamando a **SQLGetInfo** con la opción SQL_TXN_CAPABLE. Para obtener más información, vea la descripción de la función [SQLGetInfo.](../../../odbc/reference/syntax/sqlgetinfo-function.md)  
  
 Si el controlador no admite transacciones pero la aplicación tiene la capacidad (mediante una API que no sea ODBC) para bloquear y desbloquear datos, las aplicaciones pueden lograr compatibilidad con transacciones bloqueando y desbloqueando registros y tablas según sea necesario. Para implementar el ejemplo de transferencia de cuenta, la aplicación bloquearía los registros de ambas cuentas, copiaría los valores actuales, cargaría la primera cuenta, abonaría la segunda cuenta y desbloquearía los registros. Si se produce un error en cualquier paso, la aplicación restablecería las cuentas mediante las copias.  
  
 Incluso los orígenes de datos que admiten transacciones podrían no ser capaces de admitir más de una transacción a la vez dentro de un entorno determinado. Las aplicaciones llaman a **SQLGetInfo** con la opción SQL_MULTIPLE_ACTIVE_TXN para determinar si un origen de datos puede admitir transacciones activas simultáneas en más de una conexión en el mismo entorno. Dado que hay una transacción por conexión, esto solo es interesante para las aplicaciones que tienen varias conexiones al mismo origen de datos.
