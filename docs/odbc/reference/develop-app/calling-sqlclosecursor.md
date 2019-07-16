---
title: Al llamar a SQLCloseCursor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application upgrades [ODBC], SQLCloseCursor
- backward compatibility [ODBC], SqlCloseCursor
- SQLCloseCursor function [ODBC], calling
- upgrading applications [ODBC], SQLCloseCursor
- compatibility [ODBC], SQLCloseCursor
ms.assetid: ef448c39-a9ad-4f07-8ef3-65bd4cef672a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 447a0892049317813fa9fe6986e6219922a11e28
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068691"
---
# <a name="calling-sqlclosecursor"></a>Al llamar a SQLCloseCursor
Dado que **SQLCloseCursor** es prácticamente el mismo que **SQLFreeStmt** con SQL_CLOSE, el Administrador de controladores no se asigna esta función. Se asignan las funciones de reemplazo para que existente ODBC *2.x* aplicaciones pueden mover fácilmente a ODBC *3.x* mediante el uso de las nuevas funciones. Este movimiento resulta más fácil para dichas aplicaciones empezar a usar ODBC nuevo *3.x* funcionalidad dentro de código condicional de manera modular. **SQLCloseCursor** no representa ninguna funcionalidad nueva. Una aplicación no obtener cualquier ventaja moviendo a **SQLCloseCursor** desde **SQLFreeStmt** con SQL_CLOSE.
