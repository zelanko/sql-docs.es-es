---
description: Confirmación y el comportamiento de reversión
title: Comportamiento de commit y rollback | Microsoft Docs
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
ms.assetid: 2ac8f012-e46d-41ca-81bb-e4a3246e3241
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 309d28dfb2c97fc8f3d8631edc3f0f7b9db85508
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494674"
---
# <a name="commit-and-rollback-behavior"></a>Confirmación y el comportamiento de reversión
Un comportamiento común entre los DBMS de servidor es cerrar los cursores y descartar las instrucciones preparadas cuando una instrucción se confirma o se revierte. Es más probable que las bases de datos de escritorio mantengan los cursores abiertos y mantengan las instrucciones preparadas. Para obtener más información, vea las opciones SQL_CURSOR_COMMIT_BEHAVIOR y SQL_CURSOR_ROLLBACK_BEHAVIOR en la descripción de la función [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) y el [efecto de las transacciones en los cursores y las instrucciones preparadas](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md).
