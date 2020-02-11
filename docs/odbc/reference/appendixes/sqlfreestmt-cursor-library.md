---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4bfe5c91a90f874b514abb661ea06631be87e69c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68086413"
---
# <a name="sqlfreestmt-cursor-library"></a>SQLFreeStmt (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en los nuevos trabajos de desarrollo y planee modificar las aplicaciones que actualmente la utilizan. Microsoft recomienda el uso de la funcionalidad de cursor del controlador.  
  
 En este tema se describe el uso de la función **SQLFreeStmt** en la biblioteca de cursores. Para obtener información general sobre **SQLFreeStmt**, consulte la [función SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md).  
  
 Si una aplicación llama a **SQLFreeStmt** con la opción SQL_UNBIND después de llamar a **SQLExtendedFetch**, **SQLFetch**o **SQLFetchScroll**, la biblioteca de cursores devuelve un error. Antes de poder desenlazar las columnas del conjunto de resultados, una aplicación debe llamar a **SQLCloseCursor** o **SQLFreeStmt** con la opción SQL_CLOSE.
