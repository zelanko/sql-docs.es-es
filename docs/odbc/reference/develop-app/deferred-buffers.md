---
title: Búferes diferidos ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- buffers [ODBC], deferred
- deferred buffers [ODBC]
ms.assetid: 02c9a75c-2103-4f68-a1db-e31f7e0f1f03
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f34c6d3d886a0a75c309dc4f5c71f5c7ba3df447
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305986"
---
# <a name="deferred-buffers"></a>Búferes diferidos
Un *búfer diferido* es aquel cuyo valor se utiliza en algún momento *después* de que se especifica en una llamada de función. Por ejemplo, **SQLBindParameter** se utiliza para asociar o *enlazar* un búfer de datos con un parámetro en una instrucción SQL. La aplicación especifica el número del parámetro y pasa la dirección, la longitud de bytes y el tipo del búfer. El controlador guarda esta información, pero no examina el contenido del búfer. Más adelante, cuando la aplicación ejecuta la instrucción, el controlador recupera la información y la utiliza para recuperar los datos del parámetro y enviarla al origen de datos. Por lo tanto, se aplaza la entrada de datos en el búfer. Dado que los búferes diferidos se especifican en una función y se utilizan en otra, es un error de programación de aplicaciones liberar un búfer diferido mientras el controlador todavía espera que exista; para obtener más información, consulte [Asignación y liberación](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md)de búferes , más adelante en esta sección.  
  
 Los búferes de entrada y salida se pueden aplazar. En la tabla siguiente se resumen los usos de búferes diferidos. Tenga en cuenta que los búferes diferidos enlazados a columnas de conjunto de resultados se especifican con **SQLBindCol**y los búferes diferidos enlazados a parámetros de instrucción SQL se especifican con **SQLBindParameter**.  
  
|Uso del búfer|Tipo|Especificado con|Usado por|  
|----------------|----------|--------------------|-------------|  
|Envío de datos para parámetros de entrada|Entrada diferida|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|Envío de datos para actualizar o insertar una fila en un conjunto de resultados|Entrada diferida|**SQLBindCol**|**SQLSetPos**|  
|Devolución de datos para los parámetros de salida y entrada/salida|Salida diferida|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|Devolución de datos del conjunto de resultados|Salida diferida|**SQLBindCol**|**SQLFetch**<br /> **SQLFetchScroll SQLSetPos**|
