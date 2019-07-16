---
title: Aplaza búferes | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1f7c90dacc375877b4e449b8d59533ce75ff8a4e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68076830"
---
# <a name="deferred-buffers"></a>Búferes diferidos
Un *búferes diferidos* es uno cuyo valor se utiliza en algún momento *después* se especifica en una llamada de función. Por ejemplo, **SQLBindParameter** se usa para asociar, o *enlazar,* un búfer de datos con un parámetro en una instrucción SQL. La aplicación especifica el número del parámetro y pasa la dirección, la longitud de bytes y el tipo del búfer. El controlador guarda esta información, pero no examina el contenido del búfer. Más adelante, cuando la aplicación ejecuta la instrucción, el controlador recupera la información y lo usa para recuperar los datos del parámetro y enviarlo al origen de datos. Por lo tanto, se aplaza la entrada de datos en el búfer. Dado que búferes diferidos se especifica en una función y se usa en otro, es un error de programación de aplicaciones para liberar un búfer aplazado mientras el controlador todavía espera que exista; Para obtener más información, consulte [asignar y liberar búferes](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md), más adelante en esta sección.  
  
 Se pueden aplazar los búferes de entrada y salidos. En la tabla siguiente se resume los usos de búferes diferidos. Tenga en cuenta que se han especificado búferes diferidos enlazados como resultado columnas del conjunto con **SQLBindCol**, y se especifican los búferes diferidos enlazados a los parámetros de la instrucción SQL con **SQLBindParameter**.  
  
|Uso del búfer|Type|Especificado con|Usado por|  
|----------------|----------|--------------------|-------------|  
|Envío de datos para los parámetros de entrada|Entradas aplazada|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|Envío de datos para actualizar o insertar una fila en un resultado de conjunto|Entradas aplazada|**SQLBindCol**|**SQLSetPos**|  
|Devolver datos de salida y parámetros de entrada/salida|Salida diferida|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|Devuelve el resultado de establece los datos|Salida diferida|**SQLBindCol**|**SQLFetch**<br /> **SQLFetchScroll SQLSetPos**|
