---
title: Llamar a SQLCloseCursor ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2feab58de28e39747a1d9c819f9f15426b156151
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306279"
---
# <a name="calling-sqlclosecursor"></a>Al llamar a SQLCloseCursor
Dado que **SQLCloseCursor** es casi el mismo que **SQLFreeStmt** con SQL_CLOSE, el Administrador de controladores no asigna esta función. Las funciones de reemplazo se asignan para que las aplicaciones ODBC *2.x* existentes puedan moverse fácilmente a ODBC *3.x* mediante las nuevas funciones. Tal movimiento hace que sea más fácil para este tipo de aplicaciones comenzar a usar la nueva funcionalidad ODBC *3.x* dentro del código condicional de una manera modular. **SQLCloseCursor** no representa ninguna funcionalidad nueva. Una aplicación no obtiene ninguna ventaja al pasar a **SQLCloseCursor** de **SQLFreeStmt** con SQL_CLOSE.
