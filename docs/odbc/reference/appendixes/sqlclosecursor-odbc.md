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
manager: craigg
ms.openlocfilehash: 827f7195c5d4eb4f67cb3298b75519a5583053d1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47715123"
---
# <a name="sqlclosecursorodbc"></a>SQLCloseCursor_ODBC
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad de cursor del controlador.  
  
 Este tema describe el uso de la **SQLCloseCursor** función en la biblioteca de cursores. Para obtener información general sobre **SQLCloseCursor**, consulte [función SQLCloseCursor](../../../odbc/reference/syntax/sqlclosecursor-function.md).  
  
 La biblioteca de cursores no se admite llamar a **SQLCloseCursor** sin un cursor abierto. Intentar esto devolverá SQLSTATE 24000 (estado de cursor no válido). Una llamada a **SQLFreeStmt** con un *opción* de SQL_CLOSE cuando el cursor no está abierto es compatible con la biblioteca de cursores.
