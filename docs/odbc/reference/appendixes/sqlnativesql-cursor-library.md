---
title: SQLNativeSql (biblioteca de cursores) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLNativeSql function [ODBC], Cursor Library
ms.assetid: c4459092-1177-4b2a-b7f5-e0083d3bf2b2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c5b87f64963e7b0ad45fbec33e410165cd0c9723
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63298491"
---
# <a name="sqlnativesql-cursor-library"></a>SQLNativeSql (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad de cursor del controlador.  
  
 Este tema describe el uso de la **SQLNativeSql** función en la biblioteca de cursores. Para obtener información general sobre **SQLNativeSql**, consulte [función SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md).  
  
 Si el controlador es compatible con esta función, se llama la biblioteca de cursores **SQLNativeSql** en el controlador y lo pasa la instrucción SQL. Para una actualización posicionada, coloca la eliminación, y **seleccione para actualizar** instrucciones, la biblioteca de cursores modifica la instrucción antes de pasarlo al controlador.  
  
> [!NOTE]  
>  La biblioteca de cursores devuelve incorrectamente SQLSTATE 34000 (nombre de cursor no válido) si el nombre del cursor no es válido en una actualización por posición o la instrucción delete que se pasa el *InStatementText* argumento de **SQLNativeSql** . **SQLNativeSql** no está diseñada para devolver errores de sintaxis, que se devuelven solo de acuerdo con la preparación o ejecución.
