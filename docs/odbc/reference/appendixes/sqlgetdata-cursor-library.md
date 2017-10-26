---
title: SQLGetData (biblioteca de cursores) | Documentos de Microsoft
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
- SQLGetData function [ODBC], Cursor Library
ms.assetid: ff40c9c0-b847-4426-a099-1bff47e6e872
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 19aa94323ee9ad9655e374bd3fe466fcb78f3c48
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetdata-cursor-library"></a>SQLGetData (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 Este tema describe el uso de la **SQLGetData** función en la biblioteca de cursores. Para obtener información general sobre **SQLGetData**, consulte [función SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md).  
  
 La biblioteca de cursores implementa **SQLGetData** construyendo primero un **seleccione** instrucción con un **donde** cláusula que enumera los valores almacenados en su caché para cada límite columna de la fila actual. A continuación, ejecuta el **seleccione** instrucción para volver a seleccionar las filas y las llamadas **SQLGetData** en el controlador para recuperar los datos del origen de datos (en lugar de la memoria caché).  
  
> [!CAUTION]  
>  El **donde** cláusula construido por la biblioteca de cursores para identificar la fila actual no puede identificar las filas, identificar una fila diferente o más de una fila. Para obtener más información, consulte [construir instrucciones buscar](../../../odbc/reference/appendixes/constructing-searched-statements.md).  
  
 Si se establece el atributo de instrucción de SQL_ATTR_USE_BOOKMARKS en SQL_UB_VARIABLE, **SQLGetData** puede llamarse en 0 para devolver los datos de marcador de columna.  
  
 Las llamadas a **SQLGetData** están sujetos a las restricciones siguientes:  
  
-   **SQLGetData** no se puede llamar para cursores de solo avance.  
  
-   **SQLGetData** se puede llamar solo cuando se cumplen las condiciones siguientes: una **seleccione** instrucción genera el conjunto de resultados; el **seleccione** instrucción no contenía una combinación, un ** Unión** cláusula, o un **GROUP BY** cláusula; y columnas que utilicen un alias o una expresión en la lista select no se enlazaron con **SQLBindCol**.  
  
-   Si el controlador admite solo una instrucción activa, la biblioteca de cursores captura el resto del resultado establecer antes de ejecutar el **seleccione** instrucción y llamar al método **SQLGetData**.

