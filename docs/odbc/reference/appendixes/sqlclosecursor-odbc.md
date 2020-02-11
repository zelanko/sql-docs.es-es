---
title: SQLCloseCursor_ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLCloseCursor function [ODBC], ODBC
ms.assetid: 5e47e3f7-e1b8-451f-bf75-daa19b7c7271
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a4d0f88d2d9eaba7d95ba887ffbe11e728320b17
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68123380"
---
# <a name="sqlclosecursor_odbc"></a>SQLCloseCursor_ODBC
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en los nuevos trabajos de desarrollo y planee modificar las aplicaciones que actualmente la utilizan. Microsoft recomienda el uso de la funcionalidad de cursor del controlador.  
  
 En este tema se describe el uso de la función **SQLCloseCursor** en la biblioteca de cursores. Para obtener información general sobre **SQLCloseCursor**, consulte la [función SQLCloseCursor](../../../odbc/reference/syntax/sqlclosecursor-function.md).  
  
 La biblioteca de cursores no admite la llamada a **SQLCloseCursor** sin un cursor abierto. Si intenta hacerlo, se devolverá SQLSTATE 24000 (estado de cursor no válido). La llamada a **SQLFreeStmt** con una *opción* de SQL_CLOSE cuando no hay ningún cursor abierto es compatible con la biblioteca de cursores.
