---
title: SQLSetScrollOptions (biblioteca de cursores) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Cursor Library
ms.assetid: c5c0ac6d-a6c1-4077-8186-1644df1944f8
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 96041fdfcf9dbad53513f402faad8b2aeaf37cf3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetscrolloptions-cursor-library"></a>SQLSetScrollOptions (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 Este tema describe el uso de la **SQLSetScrollOptions** función en la biblioteca de cursores. Para obtener información general sobre **SQLSetScrollOptions**, consulte [SQLSetScrollOptions función](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md).  
  
 La biblioteca de cursores es compatible con **SQLSetScrollOptions** solo por compatibilidad con versiones anteriores; aplicaciones deben utilizar los atributos de instrucción SQL_ATTR_ROW_ARRAY_SIZE, SQL_ATTR_CURSOR_TYPE y SQL_ATTR_CONCURRENCY en su lugar.
