---
title: Construcción de instrucciones Searched | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- searched statements [ODBC]
- ODBC cursor library [ODBC], statement processing
- ODBC cursor library [ODBC], searched statements
- SQL statements [ODBC], cursor library
- cursor library [ODBC], statement processing
- cursor library [ODBC], searched statements
- SQL statements [ODBC], searched statements
ms.assetid: e429254c-c43f-4fbf-98b2-5f1ed53501ff
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 616e4241c6d28e846a56116a70e79254e13dd5fb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63224567"
---
# <a name="constructing-searched-statements"></a>Construcción de instrucciones Searched
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad de cursor del controlador.  
  
 Para admitir la actualización posicionada e instrucciones delete, la biblioteca de cursores construye una búsqueda **actualizar** o **eliminar** instrucción desde la instrucción posicionada. Para admitir llamadas a **SQLGetData** en un bloque de datos, la biblioteca de cursores construye una búsqueda **seleccione** instrucción para crear un resultado de conjunto que contiene la fila de datos actual. En cada una de estas instrucciones, el **donde** enumera los valores almacenados en la memoria caché para cada columna enlazada que devuelve SQL_PRED_SEARCHABLE o SQL_PRED_BASIC para el identificador de campo SQL_DESC_SEARCHABLE en la cláusula  **SQLColAttribute**.  
  
> [!CAUTION]  
>  El **donde** cláusula construido por la biblioteca de cursores para identificar la fila actual no puede identificar las filas, identificar una fila diferente o más de una fila.  
  
 Si una instrucción de eliminación o actualización posicionada afecta a más de una fila, la biblioteca de cursores actualiza la matriz de Estados de fila solo para la fila en el que se coloca el cursor y devuelve SQL_SUCCESS_WITH_INFO y SQLSTATE 01001 (conflicto de operación de Cursor). Si la instrucción no identifica las filas, la biblioteca de cursores no actualiza la matriz de Estados de fila y devuelve SQL_SUCCESS_WITH_INFO y SQLSTATE 01001 (conflicto de operación de Cursor). Una aplicación puede llamar a **SQLRowCount** para determinar el número de filas que se han actualizado o eliminado.  
  
 Si el **seleccione** cláusula que se utiliza para situar el cursor para una llamada a **SQLGetData** identifica más de una fila, **SQLGetData** no se garantiza para devolver los datos correctos. Si no identifica ninguna fila, **SQLGetData** devuelve SQL_NO_DATA.  
  
 Si una aplicación se ajusta a las instrucciones siguientes, el **donde** cláusula construido por la biblioteca de cursores debe identificar de forma exclusiva la fila actual, excepto cuando es imposible, como cuando el origen de datos contiene duplicado filas.  
  
-   **Enlazar las columnas que identifican de forma única la fila.** Si las columnas enlazadas no identificar de forma exclusiva la fila, el **donde** cláusula construido por la biblioteca de cursores podría identificar más de una fila. En una instrucción de eliminación o actualización posicionada, una cláusula de ese tipo puede provocar más de una fila para actualizarse o eliminarse. En una llamada a **SQLGetData**, una cláusula de ese tipo puede provocar que el controlador obtener datos de la fila incorrecta. Enlazar todas las columnas en una clave única, se garantiza que cada fila tiene una identificación exclusiva.  
  
-   **Asignar búferes de datos lo suficientemente grandes que se produce ningún truncamiento.** Caché de la biblioteca de cursores es una copia de los valores de los búferes de conjunto de filas enlazados en el conjunto de resultados con **SQLBindCol**. Si los datos se truncan cuando se coloca en estos búferes, también se truncará en la memoria caché. Un **donde** cláusula construido a partir de los valores de truncado no podría identificar correctamente la fila del origen de datos subyacente.  
  
-   **Especifique los búferes de longitud distinto de null para los datos binarios de C.** La biblioteca de cursores asigna búferes de longitud en Sí si solo de la memoria caché el *StrLen_or_IndPtr* argumento en **SQLBindCol** es distinto de null. Cuando el *TargetType* argumento es SQL_C_BINARY, la biblioteca de cursores requiere la longitud de los datos binarios para construir un **donde** cláusula de los datos. Si no hay ningún búfer de longitud para una columna SQL_C_BINARY y la aplicación llama a **SQLGetData** o intenta ejecutar una actualización por posición o la instrucción delete, devuelve la biblioteca de cursores SQL_ERROR y SQLSTATE SL014 (una posición se emitió la solicitud y no todos los campos de número de columna se almacena en búfer).  
  
-   **Especifique los búferes de longitud distinto de null para las columnas que aceptan valores NULL.** La biblioteca de cursores asigna búferes de longitud en Sí si solo de la memoria caché el *StrLen_or_IndPtr* argumento en **SQLBindCol** es distinto de null. Porque SQL_NULL_DATA se almacena en el búfer de longitud, la biblioteca de cursores se supone que cualquier columna para cuya longitud no se especifica el búfer es distinto de NULL. Si no hay ninguna columna de longitud se especifica para una columna que acepta valores NULL, la biblioteca de cursores crea un **donde** cláusula que usa el valor de datos para la columna. Esta cláusula no identificará correctamente la fila.
