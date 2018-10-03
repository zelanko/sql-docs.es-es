---
title: Ejecutar coloca instrucciones Update y Delete | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2391c01d93c876562ab9d870ab0dba22bf74cea5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47772053"
---
# <a name="executing-positioned-update-and-delete-statements"></a>Ejecución de instrucciones de eliminación y actualización Positioned
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad de cursor del controlador.  
  
 Después de una aplicación ha capturado un bloque de datos con **SQLFetchScroll**, puede actualizar o eliminar los datos en el bloque. Para ejecutar una actualización por posición o delete, la aplicación:  
  
1.  Las llamadas **SQLSetPos** para colocar el cursor en la fila para actualizarse o eliminarse.  
  
2.  Crea una actualización por posición o la instrucción delete con la sintaxis siguiente:  
  
     **ACTUALIZACIÓN** *nombre de tabla*  
  
     **ESTABLECER** *identificador de columna* **=** {*expresión* &#124; **NULL**}  
  
     [**,** *identificador de columna* **=** {*expresión* &#124; **NULL**}]  
  
     **WHERE CURRENT OF** *nombre de cursor*  
  
     **DELETE FROM** *nombre-tabla* **WHERE CURRENT OF** *nombre de cursor*  
  
     La manera más fácil de construir el **establecer** cláusula en una instrucción de actualización posicionada consiste en usar marcadores de parámetros para cada columna se puede actualizar y usar **SQLBindParameter** para enlazar a los búferes del conjunto de filas de la se actualizó la fila. En este caso, el tipo de datos de C del parámetro será el mismo que el tipo de datos de C del búfer del conjunto de filas.  
  
3.  Actualiza los búferes del conjunto de filas de la fila actual si se ejecutará una instrucción update posicionadas. Después de ejecutar correctamente una instrucción de actualización por posición, la biblioteca de cursores copia los valores de cada columna en la fila actual a su memoria caché.  
  
    > [!CAUTION]  
    >  Si la aplicación no actualizar correctamente los búferes del conjunto de filas antes de ejecutar una instrucción de actualización posicionada, los datos en la memoria caché serán incorrectos después de ejecutar la instrucción.  
  
4.  Ejecuta la actualización por posición o la instrucción delete usando una instrucción diferente que la instrucción asociada con el cursor.  
  
    > [!CAUTION]  
    >  El **donde** cláusula construido por la biblioteca de cursores para identificar la fila actual no puede identificar las filas, identificar una fila diferente o más de una fila. Para obtener más información, consulte [construir busca instrucciones](../../../odbc/reference/appendixes/constructing-searched-statements.md).  
  
 Toda actualización por posición y las instrucciones delete requieren un nombre de cursor. Para especificar el nombre del cursor, una aplicación llama a **SQLSetCursorName** antes de abrir el cursor. Para usar el nombre del cursor generado por el controlador, una aplicación llama a **SQLGetCursorName** después de abrir el cursor.  
  
 Después del cursor biblioteca ejecuta una actualización por posición o la instrucción delete, la matriz de estado, búferes de conjunto de filas y caché mantenida por la biblioteca de cursores contienen los valores mostrados en la tabla siguiente.  
  
|Instrucción que se utiliza|Valor de matriz de estado de fila|Valores de<br /><br /> búferes del conjunto de filas|Valores de<br /><br /> búferes de memoria caché|  
|--------------------|-------------------------------|----------------------------------|---------------------------------|  
|Actualización posicionada|SQL_ROW_UPDATED|Nuevos valores [1]|Nuevos valores [1]|  
|Delete posicionada|SQL_ROW_DELETED|Valores antiguos|Valores antiguos|  
  
 [1] en la aplicación debe actualizar los valores de los búferes de conjunto de filas antes de ejecutar la instrucción de actualización por posición; Después de ejecutar la instrucción de actualización por posición, la biblioteca de cursores copia los valores de los búferes de conjunto de filas en su memoria caché.
