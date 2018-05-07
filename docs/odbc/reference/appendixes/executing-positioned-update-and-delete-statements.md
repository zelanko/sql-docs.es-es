---
title: Ejecutar coloca instrucciones Update y Delete | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- cursor library [ODBC], positioned update or delete
- positioned updates [ODBC]
- ODBC cursor library [ODBC], positioned update or delete
ms.assetid: 1d64f309-2a6e-4ad1-a6b5-e81145549c56
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e7099999311d565af4eeff5943306c927d81f3b9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="executing-positioned-update-and-delete-statements"></a>Ejecutar instrucciones de eliminación y actualización posicionada
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 Después de que una aplicación ha capturado un bloque de datos con **SQLFetchScroll**, puede actualizar o eliminar los datos en el bloque. Para ejecutar una actualización por posición o delete, la aplicación:  
  
1.  Llamadas **SQLSetPos** para colocar el cursor en la fila para actualizarse o eliminarse.  
  
2.  Construye una actualización por posición o la instrucción delete con la sintaxis siguiente:  
  
     **ACTUALIZACIÓN** *nombre de la tabla*  
  
     **ESTABLECER** *identificador de la columna* **=** {*expresión* &#124; **NULL**}  
  
     [**,** *identificador de la columna* **=** {*expresión* &#124; **NULL**}]  
  
     **WHERE CURRENT OF** *nombre del cursor*  
  
     **DELETE FROM** *nombre de la tabla* **WHERE CURRENT OF** *nombre del cursor*  
  
     La manera más fácil de construir el **establecer** cláusula en una instrucción de actualización posicionada consiste en utilizar marcadores de parámetros para cada columna que se actualizarán y usar **SQLBindParameter** para enlazar a los búferes del conjunto de filas de la se actualizó la fila. En este caso, el tipo de datos de C del parámetro será el mismo que el tipo de datos de C del búfer del conjunto de filas.  
  
3.  Actualiza los búferes de conjunto de filas de la fila actual si se ejecutará una instrucción update posicionadas. Después de ejecutar correctamente una instrucción de actualización por posición, la biblioteca de cursores copia los valores de cada columna en la fila actual en su memoria caché.  
  
    > [!CAUTION]  
    >  Si la aplicación no actualiza correctamente los búferes de conjunto de filas antes de ejecutar una instrucción de actualización por posición, los datos en la memoria caché serán incorrectos después de ejecutar la instrucción.  
  
4.  Ejecuta la actualización por posición o la instrucción delete usando una instrucción diferente que la instrucción asociada con el cursor.  
  
    > [!CAUTION]  
    >  El **donde** cláusula construido por la biblioteca de cursores para identificar la fila actual no puede identificar las filas, identificar una fila diferente o más de una fila. Para obtener más información, consulte [construir instrucciones buscar](../../../odbc/reference/appendixes/constructing-searched-statements.md).  
  
 Todos actualización por posición y las instrucciones delete requieren un nombre de cursor. Para especificar el nombre del cursor, llama a una aplicación **SQLSetCursorName** antes de abrir el cursor. Para usar el nombre del cursor generado por el controlador, una aplicación llama **SQLGetCursorName** una vez que se abre el cursor.  
  
 Después del cursor biblioteca ejecuta una actualización por posición o instrucción delete, la matriz de estado, búferes de conjunto de filas y caché mantenida por la biblioteca de cursores contienen los valores mostrados en la tabla siguiente.  
  
|Instrucción que se utiliza|Valor de matriz de Estados de fila|Valores de<br /><br /> búferes de conjunto de filas|Valores de<br /><br /> búferes de memoria caché|  
|--------------------|-------------------------------|----------------------------------|---------------------------------|  
|Actualización posicionada|SQL_ROW_UPDATED|Nuevos valores [1]|Nuevos valores [1]|  
|Delete posicionada|SQL_ROW_DELETED|Valores antiguos|Valores antiguos|  
  
 [1] en la aplicación debe actualizar los valores de los búferes de conjunto de filas antes de ejecutar la instrucción de actualización por posición; Después de ejecutar la instrucción de actualización por posición, la biblioteca de cursores copia los valores de los búferes de conjunto de filas a su memoria caché.
