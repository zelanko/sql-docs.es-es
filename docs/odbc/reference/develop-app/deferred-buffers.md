---
title: "Diferida búferes | Documentos de Microsoft"
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
- buffers [ODBC], deferred
- deferred buffers [ODBC]
ms.assetid: 02c9a75c-2103-4f68-a1db-e31f7e0f1f03
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 94d240284ce0273e0700bfbabfb38fd0a41884cf
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="deferred-buffers"></a>Búferes diferidos
A *búfer diferida* es uno cuyo valor se utiliza en algún momento *después* se especifica en una llamada de función. Por ejemplo, **SQLBindParameter** se usa para asociar, o *enlazar,* un búfer de datos con un parámetro en una instrucción SQL. La aplicación especifica el número del parámetro y pasa la dirección, la longitud de bytes y el tipo de búfer. El controlador guarda esta información pero no examina el contenido del búfer. Más adelante, cuando la aplicación ejecuta la instrucción, el controlador recupera la información y lo utiliza para recuperar los datos del parámetro y enviarlo al origen de datos. Por lo tanto, se pospone la entrada de datos en el búfer. Porque búferes diferidos se especificado en una función y se usa en el otro, es un error de programación de aplicaciones para liberar un búfer aplazado mientras el controlador de espera que todavía que exista; Para obtener más información, consulte [asignar y liberar búferes](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md), más adelante en esta sección.  
  
 Búferes de entrada y salidos se pueden aplazar. En la tabla siguiente se resume los usos de búferes diferidos. Tenga en cuenta que se especifican búferes aplazados enlazados a columnas del conjunto de resultado con **SQLBindCol**, y se especifican búferes aplazados enlazados a los parámetros de la instrucción SQL con **SQLBindParameter**.  
  
|Uso de búfer|Tipo|Especificado con|Usado por|  
|----------------|----------|--------------------|-------------|  
|Enviar datos de parámetros de entrada|Entrada diferida|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|Envía datos al actualizar o insertar una fila en un resultado de conjunto|Entrada diferida|**SQLBindCol**|**SQLSetPos**|  
|Devolver datos de salida y los parámetros de entrada/salida|Salida de diferida|**SQLBindParameter**|**SQLExecute**<br /> **SQLExecDirect**|  
|Devolver resultados establece datos|Salida de diferida|**SQLBindCol**|**SQLFetch**<br /> **SQLFetchScroll SQLSetPos**|
