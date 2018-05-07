---
title: SQLNativeSql (biblioteca de cursores) | Documentos de Microsoft
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
- SQLNativeSql function [ODBC], Cursor Library
ms.assetid: c4459092-1177-4b2a-b7f5-e0083d3bf2b2
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b33e8112e178770320a5f5f57edf2e1971036301
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlnativesql-cursor-library"></a>SQLNativeSql (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 Este tema describe el uso de la **SQLNativeSql** función en la biblioteca de cursores. Para obtener información general sobre **SQLNativeSql**, consulte [SQLNativeSql, función](../../../odbc/reference/syntax/sqlnativesql-function.md).  
  
 Si el controlador es compatible con esta función, llama a la biblioteca de cursores **SQLNativeSql** en el controlador y le pasa la instrucción SQL. Para actualización posicionada, coloca delete, y **seleccione para actualizar** instrucciones, la biblioteca de cursores modifica la instrucción antes de pasar al controlador.  
  
> [!NOTE]  
>  La biblioteca de cursores incorrectamente devuelve SQLSTATE 34000 (nombre de cursor no válido) si el nombre del cursor no es válido en una actualización por posición o una instrucción delete que se pasa en el *InStatementText* argumento de **SQLNativeSql** . **SQLNativeSql** no está diseñada para devolver errores de sintaxis, que se devuelven solo cuando la preparación o ejecución.
