---
title: Llamando a SQLCloseCursor | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68068691"
---
# <a name="calling-sqlclosecursor"></a>Al llamar a SQLCloseCursor
Dado que **SQLCloseCursor** es casi igual que **SQLFreeStmt** con SQL_CLOSE, el administrador de controladores no asigna esta función. Las funciones de reemplazo se asignan de modo que las aplicaciones ODBC *2. x* existentes se puedan trasladar fácilmente a ODBC *3. x* mediante el uso de las nuevas funciones. Este tipo de movimiento facilita que estas aplicaciones empiecen a usar la nueva funcionalidad ODBC *3. x* dentro del código condicional de manera modular. **SQLCloseCursor** no representa ninguna funcionalidad nueva. Una aplicación no obtiene ninguna ventaja al pasar a **SQLCloseCursor** desde **SQLFreeStmt** con SQL_CLOSE.
