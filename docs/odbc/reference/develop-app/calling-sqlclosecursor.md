---
description: Al llamar a SQLCloseCursor
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 925617d79266f0b50ef9b38586b31af91311b63e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494775"
---
# <a name="calling-sqlclosecursor"></a>Al llamar a SQLCloseCursor
Dado que **SQLCloseCursor** es casi igual que **SQLFreeStmt** con SQL_CLOSE, el administrador de controladores no asigna esta función. Las funciones de reemplazo se asignan de modo que las aplicaciones ODBC *2. x* existentes se puedan trasladar fácilmente a ODBC *3. x* mediante el uso de las nuevas funciones. Este tipo de movimiento facilita que estas aplicaciones empiecen a usar la nueva funcionalidad ODBC *3. x* dentro del código condicional de manera modular. **SQLCloseCursor** no representa ninguna funcionalidad nueva. Una aplicación no obtiene ninguna ventaja al pasar a **SQLCloseCursor** desde **SQLFreeStmt** con SQL_CLOSE.
