---
title: Búferes diferidos | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305986"
---
# <a name="deferred-buffers"></a>Búferes diferidos
Un *búfer diferido* es aquél cuyo valor se utiliza en algún momento *después* de especificarse en una llamada de función. Por ejemplo, **SQLBindParameter** se utiliza para asociar o *enlazar* un búfer de datos con un parámetro en una instrucción SQL. La aplicación especifica el número del parámetro y pasa la dirección, la longitud de bytes y el tipo del búfer. El controlador guarda esta información, pero no examina el contenido del búfer. Más adelante, cuando la aplicación ejecuta la instrucción, el controlador recupera la información y la utiliza para recuperar los datos del parámetro y enviarlos al origen de datos. Por lo tanto, se aplaza la entrada de datos en el búfer. Dado que los búferes diferidos se especifican en una función y se usan en otro, se trata de un error de programación de aplicaciones para liberar un búfer diferido mientras el controlador espera que exista; para obtener más información, vea [asignar y liberar búferes](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md), más adelante en esta sección.  
  
 Se pueden diferir los búferes de entrada y salida. En la tabla siguiente se resumen los usos de los búferes diferidos. Tenga en cuenta que los búferes diferidos enlazados a las columnas del conjunto de resultados se especifican con **SQLBindCol**y los búferes diferidos enlazados a los parámetros de la instrucción SQL se especifican con **SQLBindParameter**.  
  
|Uso de búfer|Tipo|Especificado con|Usado por|  
|----------------|----------|--------------------|-------------|  
|Enviar datos para parámetros de entrada|Entrada diferida|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|Enviar datos para actualizar o insertar una fila en un conjunto de resultados|Entrada diferida|**SQLBindCol**|**SQLSetPos**|  
|Devolver datos para los parámetros de salida y de entrada/salida|Salida diferida|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|Devolver datos del conjunto de resultados|Salida diferida|**SQLBindCol**|**SQLFetch**<br /> **SQLFetchScroll SQLSetPos**|
