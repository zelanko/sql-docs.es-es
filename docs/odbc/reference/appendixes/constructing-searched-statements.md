---
title: Construyendo declaraciones buscadas ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b8b9a27aa9fc84aadc6659993de3e12e269631d2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284745"
---
# <a name="constructing-searched-statements"></a>Construcción de instrucciones Searched
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite usar esta característica en el nuevo trabajo de desarrollo y planee modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del cursor del controlador.  
  
 Para admitir instrucciones de actualización y eliminación posicionadas, la biblioteca de cursores construye una instrucción **UPDATE** o **DELETE** buscada a partir de la instrucción posicionada. Para admitir llamadas a **SQLGetData** en un bloque de datos, la biblioteca de cursores construye una instrucción **SELECT** buscada para crear un conjunto de resultados que contiene la fila de datos actual. En cada una de estas instrucciones, la cláusula **WHERE** enumera los valores almacenados en la memoria caché para cada columna enlazada que devuelve SQL_PRED_SEARCHABLE o SQL_PRED_BASIC para el identificador de campo SQL_DESC_SEARCHABLE en **SQLColAttribute**.  
  
> [!CAUTION]  
>  La cláusula **WHERE** construida por la biblioteca de cursores para identificar la fila actual puede no identificar filas, identificar una fila diferente o identificar más de una fila.  
  
 Si una instrucción de actualización o eliminación posicionada afecta a más de una fila, la biblioteca de cursores actualiza la matriz de estado de fila solo para la fila en la que se coloca el cursor y devuelve SQL_SUCCESS_WITH_INFO y SQLSTATE 01001 (conflicto de operación de cursor). Si la instrucción no identifica ninguna fila, la biblioteca de cursores no actualiza la matriz de estado de fila y devuelve SQL_SUCCESS_WITH_INFO y SQLSTATE 01001 (conflicto de operación de cursor). Una aplicación puede llamar a **SQLRowCount** para determinar el número de filas que se actualizaron o eliminaron.  
  
 Si la cláusula **SELECT** utilizada para colocar el cursor para una llamada a **SQLGetData** identifica más de una fila, no se garantiza que **SQLGetData** devuelva los datos correctos. Si no identifica ninguna fila, **SQLGetData** devuelve SQL_NO_DATA.  
  
 Si una aplicación se ajusta a las siguientes directrices, la cláusula **WHERE** construida por la biblioteca de cursores debe identificar de forma única la fila actual, excepto cuando esto sea imposible, como cuando el origen de datos contiene filas duplicadas.  
  
-   **Enlazar columnas que identifican de forma única la fila.** Si las columnas enlazadas no identifican de forma exclusiva la fila, la cláusula **WHERE** construida por la biblioteca de cursores podría identificar más de una fila. En una instrucción update o delete posicionada, dicha cláusula puede hacer que se actualice o elimine más de una fila. En una llamada a **SQLGetData**, una cláusula de este tipo puede hacer que el controlador devuelva datos para la fila incorrecta. Enlazar todas las columnas de una clave única garantiza que cada fila se identifica de forma única.  
  
-   **Asigne búferes de datos lo suficientemente grandes como para que no se produzca ningún truncamiento.** La memoria caché de la biblioteca de cursores es una copia de los valores de los búferes del conjunto de filas enlazados al conjunto de resultados con **SQLBindCol**. Si los datos se truncan cuando se colocan en estos búferes, también se truncarán en la memoria caché. Es posible que una cláusula **WHERE** construida a partir de valores truncados no identifique correctamente la fila subyacente en el origen de datos.  
  
-   **Especifique búferes de longitud no nulos para datos binarios de C.** La biblioteca de cursores asigna búferes de longitud en su memoria caché solo si el *StrLen_or_IndPtr* argumento de **SQLBindCol** no es null. Cuando el *TargetType* argumento es SQL_C_BINARY, la biblioteca de cursores requiere la longitud de los datos binarios para construir una cláusula **WHERE** a partir de los datos. Si no hay ningún búfer de longitud para una columna SQL_C_BINARY y la aplicación llama a **SQLGetData** o intenta ejecutar una instrucción de actualización o eliminación posicionada, la biblioteca de cursores devuelve SQL_ERROR y SQLSTATE SL014 (se emitió una solicitud posicionada y no se almacenaron en búfer todos los campos de recuento de columnas).  
  
-   **Especifique búferes de longitud no nulos para columnas que aceptan valores NULL.** La biblioteca de cursores asigna búferes de longitud en su memoria caché solo si el *StrLen_or_IndPtr* argumento de **SQLBindCol** no es null. Dado que SQL_NULL_DATA se almacena en el búfer de longitud, la biblioteca de cursores supone que cualquier columna para la que no se especifica ningún búfer de longitud no acepta valores NULL. Si no se especifica ninguna columna de longitud para una columna que acepta valores NULL, la biblioteca de cursores construye una cláusula **WHERE** que utiliza el valor de datos de la columna. Esta cláusula no identificará correctamente la fila.
