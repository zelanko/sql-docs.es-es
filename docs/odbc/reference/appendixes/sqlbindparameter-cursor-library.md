---
title: SQLBindParameter (biblioteca de cursores) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQLBindParameter function [ODBC], Cursor Library
ms.assetid: 04c53e4c-cd1d-40b2-9997-684ebe43499f
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 45b3a0355edb0c9fbd37f7047aa0a1e6ff9a1fe8
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlbindparameter-cursor-library"></a>SQLBindParameter (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 Este tema describe el uso de la **SQLBindParameter** función en la biblioteca de cursores. Para obtener información general sobre **SQLBindParameter**, consulte [función SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md).  
  
 Una aplicación puede llamar a **SQLBindParameter** volver a enlazar parámetros, siempre y cuando el tipo de datos de C, tamaño de la columna y dígitos decimales de la columna dependiente que siguen siendo los mismos.  
  
 La biblioteca de cursores es compatible con el establecimiento del atributo de instrucción SQL_ATTR_ROW_BIND_OFFSET_PTR usar desplazamientos de enlace. (**SQLBindParameter** no tiene que llamar para este reenlace para que se produzca.)  
  
 La biblioteca de cursores es compatible con los parámetros de enlace datos en ejecución.
