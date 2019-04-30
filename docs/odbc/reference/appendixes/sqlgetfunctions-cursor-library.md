---
title: SQLGetFunctions (biblioteca de cursores) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetFunctions function [ODBC], Cursor Library
ms.assetid: 931acd12-4eb6-4a78-9a77-157a18a9a2d0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1123a6497207f40bd210edf35b9b4477bc9c7b6b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63188727"
---
# <a name="sqlgetfunctions-cursor-library"></a>SQLGetFunctions (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad de cursor del controlador.  
  
 Este tema describe el uso de la **SQLGetFunctions** función en la biblioteca de cursores. Para obtener información general sobre **SQLGetFunctions**, consulte [función SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md).  
  
 Cuando se llama a **SQLGetFunctions**, devuelve de la biblioteca de cursores que admite **SQLExtendedFetch**, **SQLFetchScroll**, **SQLSetPos**, y **SQLSetScrollOptions**, además de las funciones admitidas por el controlador.
