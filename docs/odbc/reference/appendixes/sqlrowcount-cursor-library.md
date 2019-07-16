---
title: SQLRowCount (biblioteca de cursores) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLRowCount function [ODBC], Cursor Library
ms.assetid: 781cf5a5-325e-4523-8633-d96d9e98277c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: be902866cfcf98a10af2c3741926de8b7541bb79
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125595"
---
# <a name="sqlrowcount-cursor-library"></a>SQLRowCount (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad de cursor del controlador.  
  
 Este tema describe el uso de la **SQLRowCount** función en la biblioteca de cursores. Para obtener información general sobre **SQLRowCount**, consulte [función SQLRowCount](../../../odbc/reference/syntax/sqlrowcount-function.md).  
  
 Cuando una aplicación llama **SQLRowCount** con la instrucción asociada con el cursor, la biblioteca de cursores devuelve el número de filas de datos que ha recuperado desde el controlador.  
  
 Cuando una aplicación llama **SQLRowCount** con la instrucción asociada con una actualización posicionada o una instrucción delete, la biblioteca de cursores devuelve el número de filas afectadas por la instrucción.  
  
 Cuando una aplicación llama **SQLRowCount** después de un **seleccione** la biblioteca de cursores de instrucción, devuelve -1.
