---
title: La confirmación y el comportamiento de la reversión | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- interoperability [ODBC], transaction support
- transactions [ODBC], DBMS support
ms.assetid: 2ac8f012-e46d-41ca-81bb-e4a3246e3241
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 54dc518099d55193efa502887c9b89308d40b75f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="commit-and-rollback-behavior"></a>Confirmación y el comportamiento de reversión
Es un comportamiento común entre servidor DBMS cerrar los cursores y descartar las instrucciones preparadas cuando una instrucción se confirma o revierte. Bases de datos de escritorio son más propensos a mantener cursores abiertos y mantener las instrucciones preparadas. Para obtener más información, vea las opciones SQL_CURSOR_COMMIT_BEHAVIOR y SQL_CURSOR_ROLLBACK_BEHAVIOR en el [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descripción de la función y [efecto de las transacciones en instrucciones preparadasycursores](../../../odbc/reference/develop-app/effect-of-transactions-on-cursors-and-prepared-statements.md).
