---
title: Al llamar a SQLCloseCursor | Documentos de Microsoft
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
- application upgrades [ODBC], SQLCloseCursor
- backward compatibility [ODBC], SqlCloseCursor
- SQLCloseCursor function [ODBC], calling
- upgrading applications [ODBC], SQLCloseCursor
- compatibility [ODBC], SQLCloseCursor
ms.assetid: ef448c39-a9ad-4f07-8ef3-65bd4cef672a
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3ad8a1d13091dd9413afb79b17eb701688d7f902
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="calling-sqlclosecursor"></a>Al llamar a SQLCloseCursor
Dado que **SQLCloseCursor** es prácticamente el mismo que **SQLFreeStmt** con SQL_CLOSE, el Administrador de controladores no se asigna esta función. Funciones de reemplazo son asignadas de forma que existente ODBC 2 *.x* aplicaciones pueden mover fácilmente a ODBC 3. *x* mediante el uso de las nuevas funciones. Tal proceso resulta más fácil para dichas aplicaciones empezar a usar nuevas ODBC 3. *x* funcionalidad dentro del código condicional en una forma modular. **SQLCloseCursor** no representa ninguna funcionalidad nueva. Una aplicación no consigue cualquier ventaja moviendo a **SQLCloseCursor** de **SQLFreeStmt** con SQL_CLOSE.
