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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bf9fe597f54ecb4bc82439251e2228ac5fdc4ea3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300595"
---
# <a name="sqlrowcount-cursor-library"></a>SQLRowCount (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en los nuevos trabajos de desarrollo y planee modificar las aplicaciones que actualmente la utilizan. Microsoft recomienda el uso de la funcionalidad de cursor del controlador.  
  
 En este tema se describe el uso de la función **SQLRowCount** en la biblioteca de cursores. Para obtener información general sobre **SQLRowCount**, consulte la [función SQLRowCount](../../../odbc/reference/syntax/sqlrowcount-function.md).  
  
 Cuando una aplicación llama a **SQLRowCount** con la instrucción asociada al cursor, la biblioteca de cursores devuelve el número de filas de datos que ha recuperado del controlador.  
  
 Cuando una aplicación llama a **SQLRowCount** con la instrucción asociada a una instrucción UPDATE o DELETE posicionada, la biblioteca de cursores devuelve el número de filas afectadas por la instrucción.  
  
 Cuando una aplicación llama a **SQLRowCount** después de una instrucción **Select** , la biblioteca de cursores devuelve-1.
