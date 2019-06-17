---
title: SQLGetData (biblioteca de cursores) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLGetData function [ODBC], Cursor Library
ms.assetid: ff40c9c0-b847-4426-a099-1bff47e6e872
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1e3009b4e3bed6fc871ecfd1aab4e2af2f1f1c86
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188769"
---
# <a name="sqlgetdata-cursor-library"></a>SQLGetData (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad de cursor del controlador.  
  
 Este tema describe el uso de la **SQLGetData** función en la biblioteca de cursores. Para obtener información general sobre **SQLGetData**, consulte [función SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md).  
  
 La biblioteca de cursores implementa **SQLGetData** construyendo primero un **seleccione** instrucción con un **donde** cláusula que enumera los valores almacenados en su memoria caché para cada límite columna de la fila actual. A continuación, ejecuta el **seleccione** instrucción para volver a seleccionar la fila y llama a **SQLGetData** en el controlador para recuperar los datos del origen de datos (en lugar de la memoria caché).  
  
> [!CAUTION]  
>  El **donde** cláusula construido por la biblioteca de cursores para identificar la fila actual no puede identificar las filas, identificar una fila diferente o más de una fila. Para obtener más información, consulte [construir busca instrucciones](../../../odbc/reference/appendixes/constructing-searched-statements.md).  
  
 Si se establece el atributo de instrucción SQL_ATTR_USE_BOOKMARKS en SQL_UB_VARIABLE, **SQLGetData** puede llamarse en 0 para devolver los datos de marcador de columna.  
  
 Las llamadas a **SQLGetData** están sujetos a las restricciones siguientes:  
  
-   **SQLGetData** no se puede llamar para cursores de solo avance.  
  
-   **SQLGetData** se puede llamar solo cuando se cumplen las condiciones siguientes: un **seleccione** instrucción puede generar el conjunto de resultados; el **seleccione** instrucción no contenía una combinación, un  **Unión** cláusula, o un **GROUP BY** cláusula; y las columnas que usan un alias o una expresión en la lista de selección no se enlazaron con **SQLBindCol**.  
  
-   Si el controlador admite solo una instrucción activa, la biblioteca de cursores captura el resto del conjunto de resultados antes de ejecutar el **seleccione** instrucción y llamar al método **SQLGetData**.
