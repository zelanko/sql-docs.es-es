---
title: "La confirmación y el comportamiento de la reversión | Documentos de Microsoft"
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
ms.assetid: 2ac8f012-e46d-41ca-81bb-e4a3246e3241
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7f8cecb32a5713f707a885f2004eef0fe13ae47a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="commit-and-rollback-behavior"></a>Confirmación y el comportamiento de reversión
Es un comportamiento común entre servidor DBMS cerrar los cursores y descartar las instrucciones preparadas cuando una instrucción se confirma o revierte. Bases de datos de escritorio son más propensos a mantener cursores abiertos y mantener las instrucciones preparadas. Para obtener más información, vea las opciones SQL_CURSOR_COMMIT_BEHAVIOR y SQL_CURSOR_ROLLBACK_BEHAVIOR en el [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descripción de la función y [efecto de las transacciones en instrucciones preparadasycursores](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md).
