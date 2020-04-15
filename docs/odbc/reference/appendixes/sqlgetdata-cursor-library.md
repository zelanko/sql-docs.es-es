---
title: SQLGetData (Biblioteca de cursores) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 07200d48f439c97003da7062fc218cd2f3081d1b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307846"
---
# <a name="sqlgetdata-cursor-library"></a>SQLGetData (biblioteca de cursores)
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite usar esta característica en el nuevo trabajo de desarrollo y planee modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del cursor del controlador.  
  
 En este tema se describe el uso de la función **SQLGetData** en la biblioteca de cursores. Para obtener información general sobre **SQLGetData**, vea [Función SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md).  
  
 La biblioteca de cursores implementa **SQLGetData** mediante la construcción de una instrucción **SELECT** con una cláusula **WHERE** que enumera los valores almacenados en su caché para cada columna enlazada de la fila actual. A continuación, ejecuta la instrucción **SELECT** para volver a seleccionar la fila y llama a **SQLGetData** en el controlador para recuperar los datos del origen de datos (a diferencia de la memoria caché).  
  
> [!CAUTION]  
>  La cláusula **WHERE** construida por la biblioteca de cursores para identificar la fila actual puede no identificar filas, identificar una fila diferente o identificar más de una fila. Para obtener más información, vea [Construir instrucciones buscadas](../../../odbc/reference/appendixes/constructing-searched-statements.md).  
  
 Si el atributo de instrucción SQL_ATTR_USE_BOOKMARKS se establece en SQL_UB_VARIABLE, **SQLGetData** se puede llamar en la columna 0 para devolver datos de marcador.  
  
 Las llamadas a **SQLGetData** están sujetas a las siguientes restricciones:  
  
-   **SQLGetData** no se puede llamar para cursores de solo avance.  
  
-   **SQLGetData** sólo se puede llamar cuando se cumplen las siguientes condiciones: una instrucción **SELECT** generó el conjunto de resultados; la instrucción **SELECT** no contenía una combinación, una cláusula **UNION** o una cláusula **GROUP BY;** y las columnas que utilizaban un alias o expresión en la lista de selección no estaban enlazadas con **SQLBindCol**.  
  
-   Si el controlador solo admite una instrucción active, la biblioteca de cursores recupera el resto del conjunto de resultados antes de ejecutar la instrucción **SELECT** y llamar a **SQLGetData**.
