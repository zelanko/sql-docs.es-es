---
title: SQLCloseCursor_ODBC de la casa de la Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e1b61267d093e11bf7ea25158f5dc6a29ccba6a1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296305"
---
# <a name="sqlclosecursor_odbc"></a>SQLCloseCursor_ODBC
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite usar esta característica en el nuevo trabajo de desarrollo y planee modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del cursor del controlador.  
  
 En este tema se describe el uso de la función **SQLCloseCursor** en la biblioteca de cursores. Para obtener información general sobre **SQLCloseCursor**, vea [SQLCloseCursor (Función)](../../../odbc/reference/syntax/sqlclosecursor-function.md).  
  
 La biblioteca de cursores no admite la llamada a **SQLCloseCursor** sin un cursor abierto. Al intentar esto, se devolverá SQLSTATE 24000 (estado de cursor no válido). La biblioteca de cursores admite la llamada a **SQLFreeStmt** con una *opción* de SQL_CLOSE cuando no hay ningún cursor abierto.
