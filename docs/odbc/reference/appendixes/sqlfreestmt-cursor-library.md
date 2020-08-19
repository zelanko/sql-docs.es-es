---
description: SQLFreeStmt (biblioteca de cursores)
title: SQLFreeStmt (biblioteca de cursores) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeStmt function [ODBC], Cursor Library
ms.assetid: 47bfbd4d-9453-4609-958d-1e05794cb223
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9bc9ba1bc747f2c4408c308b13924afc8b3ba875
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448995"
---
# <a name="sqlfreestmt-cursor-library"></a>SQLFreeStmt (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en los nuevos trabajos de desarrollo y planee modificar las aplicaciones que actualmente la utilizan. Microsoft recomienda el uso de la funcionalidad de cursor del controlador.  
  
 En este tema se describe el uso de la función **SQLFreeStmt** en la biblioteca de cursores. Para obtener información general sobre **SQLFreeStmt**, consulte la [función SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md).  
  
 Si una aplicación llama a **SQLFreeStmt** con la opción SQL_UNBIND después de llamar a **SQLExtendedFetch**, **SQLFetch**o **SQLFetchScroll**, la biblioteca de cursores devuelve un error. Antes de poder desenlazar las columnas del conjunto de resultados, una aplicación debe llamar a **SQLCloseCursor** o **SQLFreeStmt** con la opción SQL_CLOSE.
