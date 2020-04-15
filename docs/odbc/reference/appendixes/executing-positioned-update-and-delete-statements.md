---
title: Ejecución de instrucciones de actualización y eliminación posicionadas ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- cursor library [ODBC], positioned update or delete
- positioned updates [ODBC]
- ODBC cursor library [ODBC], positioned update or delete
ms.assetid: 1d64f309-2a6e-4ad1-a6b5-e81145549c56
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 96a1aa891ef8ba26c6c239cf35e62a8f36018e65
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307006"
---
# <a name="executing-positioned-update-and-delete-statements"></a>Ejecución de instrucciones de eliminación y actualización Positioned
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite usar esta característica en el nuevo trabajo de desarrollo y planee modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del cursor del controlador.  
  
 Después de que una aplicación ha capturado un bloque de datos con **SQLFetchScroll**, puede actualizar o eliminar los datos del bloque. Para ejecutar una actualización o eliminación posicionada, la aplicación:  
  
1.  Llama a **SQLSetPos** para colocar el cursor en la fila que se va a actualizar o eliminar.  
  
2.  Construye una instrucción de actualización o eliminación posicionada con la sintaxis siguiente:  
  
     **ACTUALIZAR** *nombre-tabla*  
  
     **SET** *column-identifier* **=** -*expresión* &#124; **NULL**?  
  
     [**,** *identificador* **=** de columna -*expresión* &#124; **NULL**]  
  
     **DONDE ACTUAL DE nombre-cursor** *cursor-name*  
  
     **DELETE FROM** *nombre-tabla* **WHERE CURRENT OF** *cursor-name*  
  
     La forma más fácil de construir la cláusula **SET** en una instrucción de actualización posicionada es usar marcadores de parámetro para cada columna que se va a actualizar y usar **SQLBindParameter** para enlazarlos a los búferes de conjunto de filas para la fila que se va a actualizar. En este caso, el tipo de datos C del parámetro será el mismo que el tipo de datos C del búfer del conjunto de filas.  
  
3.  Actualiza los búferes de conjunto de filas para la fila actual si se ejecutará una instrucción de actualización posicionada. Después de ejecutar correctamente una instrucción de actualización posicionada, la biblioteca de cursores copia los valores de cada columna de la fila actual en su caché.  
  
    > [!CAUTION]  
    >  Si la aplicación no actualiza correctamente los búferes del conjunto de filas antes de ejecutar una instrucción de actualización posicionada, los datos de la memoria caché serán incorrectos después de ejecutar la instrucción.  
  
4.  Ejecuta la instrucción update o delete posicionada utilizando una instrucción diferente a la instrucción asociada al cursor.  
  
    > [!CAUTION]  
    >  La cláusula **WHERE** construida por la biblioteca de cursores para identificar la fila actual puede no identificar filas, identificar una fila diferente o identificar más de una fila. Para obtener más información, vea [Construir instrucciones buscadas](../../../odbc/reference/appendixes/constructing-searched-statements.md).  
  
 Todas las instrucciones de actualización y eliminación posicionadas requieren un nombre de cursor. Para especificar el nombre del cursor, una aplicación llama a **SQLSetCursorName** antes de que se abra el cursor. Para usar el nombre del cursor generado por el controlador, una aplicación llama a **SQLGetCursorName** después de abrir el cursor.  
  
 Después de que la biblioteca de cursores ejecute una instrucción de actualización o eliminación posicionada, la matriz de estado, los búferes de conjunto de filas y la memoria caché mantenida por la biblioteca de cursores contienen los valores que se muestran en la tabla siguiente.  
  
|Declaración utilizada|Valor en la matriz de estado de fila|Los valores en<br /><br /> buffers de conjunto de filas|Los valores en<br /><br /> búferes de caché|  
|--------------------|-------------------------------|----------------------------------|---------------------------------|  
|Actualización posicionada|SQL_ROW_UPDATED|Nuevos valores[1]|Nuevos valores[1]|  
|Eliminación posicionada|SQL_ROW_DELETED|Valores anteriores|Valores anteriores|  
  
 [1] La aplicación debe actualizar los valores de los búferes del conjunto de filas antes de ejecutar la instrucción update posicionada; después de ejecutar la instrucción update posicionada, la biblioteca de cursores copia los valores de los búferes del conjunto de filas en su caché.
