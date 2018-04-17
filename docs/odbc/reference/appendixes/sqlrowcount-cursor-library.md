---
title: SQLRowCount (biblioteca de cursores) | Documentos de Microsoft
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
- SQLRowCount function [ODBC], Cursor Library
ms.assetid: 781cf5a5-325e-4523-8633-d96d9e98277c
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a74130031623a1198eada5e2bd62a992867c4e3a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sqlrowcount-cursor-library"></a>SQLRowCount (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 Este tema describe el uso de la **SQLRowCount** función en la biblioteca de cursores. Para obtener información general sobre **SQLRowCount**, consulte [función SQLRowCount](../../../odbc/reference/syntax/sqlrowcount-function.md).  
  
 Cuando una aplicación llama **SQLRowCount** con la instrucción asociada con el cursor, la biblioteca de cursores devuelve el número de filas de datos que ha recuperado desde el controlador.  
  
 Cuando una aplicación llama **SQLRowCount** con la instrucción asociada a una actualización por posición o una instrucción delete, la biblioteca de cursores devuelve el número de filas afectadas por la instrucción.  
  
 Cuando una aplicación llama **SQLRowCount** después de un **seleccione** instrucción, la biblioteca de cursores devuelve – 1.
