---
title: SQLBindParameter (biblioteca de cursores) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBindParameter function [ODBC], Cursor Library
ms.assetid: 04c53e4c-cd1d-40b2-9997-684ebe43499f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: eafab0f29cb4e1b7ecdfea378f9315ba29cf133f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199676"
---
# <a name="sqlbindparameter-cursor-library"></a>SQLBindParameter (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad de cursor del controlador.  
  
 Este tema describe el uso de la **SQLBindParameter** función en la biblioteca de cursores. Para obtener información general sobre **SQLBindParameter**, consulte [función SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md).  
  
 Una aplicación puede llamar a **SQLBindParameter** para volver a enlazar parámetros, siempre y cuando el tipo de datos C, tamaño de la columna y los dígitos decimales de la columna dependiente que siguen siendo los mismos.  
  
 La biblioteca de cursores es compatible con el atributo de instrucción SQL_ATTR_ROW_BIND_OFFSET_PTR utilizar desplazamientos de enlace. (**SQLBindParameter** no tiene que llamarse para este reenlace para que se produzca.)  
  
 La biblioteca de cursores es compatible con los parámetros de enlace datos en ejecución.
