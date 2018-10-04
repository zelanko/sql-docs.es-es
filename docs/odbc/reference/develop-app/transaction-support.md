---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: be133079c1b6beffd484942eb9ae058c14dd5c1f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47808943"
---
# <a name="transaction-support"></a>Compatibilidad con transacciones
El grado de compatibilidad con transacciones es definido por el controlador. ODBC está diseñada para implementarse en una base de datos de usuario único o de escritorio que no tiene necesidad de administrar varias actualizaciones a sus datos. Además, algunas bases de datos que admiten transacciones realizar por lo que solo para las instrucciones de lenguaje de manipulación de datos (DML) de SQL; hay restricciones o semántica de transacción especial con respecto al uso del lenguaje de definición de datos (DDL) cuando una transacción está activa. Es decir, puede haber compatibilidad con transacciones para varias actualizaciones simultáneas en tablas pero no para cambiar el número y la definición de tablas durante una transacción.  
  
 Una aplicación determina si se admiten las transacciones, si DDL se puede incluir en una transacción y los efectos especiales de inclusión de DDL en una transacción, mediante una llamada a **SQLGetInfo** con la opción SQL_TXN_CAPABLE. Para obtener más información, consulte el [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descripción de la función.  
  
 Si el controlador no admite transacciones, pero la aplicación tiene la capacidad (mediante una API que no sea ODBC) para bloquear y desbloquear los datos, las aplicaciones pueden lograr compatibilidad con transacciones, bloqueos y desbloqueo de registros y tablas según sea necesario. Para implementar el ejemplo de transferencia de la cuenta, la aplicación podría bloquear los registros de ambas cuentas, copie los valores actuales, la primera cuenta de débito, la segunda cuenta de crédito y desbloquear los registros. Si se produjo un error en todos los pasos, la aplicación podría restablecer las cuentas con las copias.  
  
 Orígenes de datos incluso que admiten transacciones podrían no ser capaz de admitir más de una transacción a la vez en un entorno concreto. Las aplicaciones llaman a **SQLGetInfo** con la opción SQL_MULTIPLE_ACTIVE_TXN para determinar si un origen de datos puede admitir transacciones activas simultáneas en más de una conexión en el mismo entorno. Dado que hay una transacción por conexión, esto solo es interesante para las aplicaciones que tienen varias conexiones al mismo origen de datos.
