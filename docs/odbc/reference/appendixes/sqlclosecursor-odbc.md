---
title: SQLCloseCursor_ODBC | Documentos de Microsoft
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
ms.topic: article
helpviewer_keywords:
- SQLCloseCursor function [ODBC], ODBC
ms.assetid: 5e47e3f7-e1b8-451f-bf75-daa19b7c7271
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d9df09aea21ed6a1e7768dfd04ab283a8342d355
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sqlclosecursorodbc"></a>SQLCloseCursor_ODBC
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 Este tema describe el uso de la **SQLCloseCursor** función en la biblioteca de cursores. Para obtener información general sobre **SQLCloseCursor**, consulte [SQLCloseCursor, función](../../../odbc/reference/syntax/sqlclosecursor-function.md).  
  
 La biblioteca de cursores no permite llamar a **SQLCloseCursor** sin un cursor abierto. Intentar esto devolverá SQLSTATE 24000 (estado de cursor no válido). Al llamar a **SQLFreeStmt** con una *opción* de SQL_CLOSE cuando ningún cursor está abierto es compatible con la biblioteca de cursores.
