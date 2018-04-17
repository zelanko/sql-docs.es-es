---
title: SQLGetFunctions (biblioteca de cursores) | Documentos de Microsoft
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
- SQLGetFunctions function [ODBC], Cursor Library
ms.assetid: 931acd12-4eb6-4a78-9a77-157a18a9a2d0
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1d1f4c68474c53c369b46737aa3c41c9cf7146c0
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sqlgetfunctions-cursor-library"></a>SQLGetFunctions (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 Este tema describe el uso de la **SQLGetFunctions** función en la biblioteca de cursores. Para obtener información general sobre **SQLGetFunctions**, consulte [función SQLGetFunctions](../../../odbc/reference/syntax/sqlgetfunctions-function.md).  
  
 Cuando se llama a **SQLGetFunctions**, devuelve de la biblioteca de cursores que admite **SQLExtendedFetch**, **SQLFetchScroll**, **SQLSetPos**, y **SQLSetScrollOptions**, además de las funciones admitidas por el controlador.
