---
title: Al recuperar los resultados (Basic) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result sets [ODBC], about result sets
- data sources [ODBC], result sets
- empty result sets [ODBC]
ms.assetid: 052870e3-3f3f-4f07-91da-b649348225f4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8eb98d7c17663894e1bacdc27e431d6a54f45d3b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62468672"
---
# <a name="retrieving-results-basic"></a>Al recuperar los resultados (Basic)
Un *conjunto de resultados* es un conjunto de filas del origen de datos que coincida con determinados criterios. Es una tabla conceptual que da como resultado de una consulta y que está disponible para una aplicación en formato tabular. **Seleccione** instrucciones, funciones de catálogo y algunos procedimientos para crear conjuntos de resultados. En el ejemplo siguiente, la primera instrucción SQL crea un conjunto que contiene todas las filas y todas las columnas de la tabla Orders de resultados y la segunda instrucción SQL crea un conjunto que contiene las columnas OrderID, vendedor y el estado de las filas de la tabla Orders de resultados en el que el estado es pendiente:  
  
```  
SELECT * FROM Orders  
SELECT OrderID, SalesPerson, Status FROM Orders WHERE Status = 'OPEN'  
```  
  
 Un conjunto de resultados puede estar vacío, que es diferente de ningún conjunto de resultados. Por ejemplo, la instrucción SQL siguiente crea un conjunto de resultados vacío:  
  
```  
SELECT * FROM Orders WHERE 1 = 2  
```  
  
 Un conjunto de resultados vacío no es diferente cualquier otro conjunto de resultados, salvo que no tiene ninguna fila. Por ejemplo, la aplicación puede recuperar metadatos para el conjunto de resultados, puede intentar recuperar las filas y debe cerrar el cursor sobre el conjunto de resultados.  
  
 El proceso de recuperar las filas del origen de datos y devolverlos a la aplicación se denomina *capturando*. Esta sección explica las partes básicas de ese proceso. Para obtener información acerca de temas más avanzados, como bloque y los cursores desplazables, consulte [cursores de bloque](../../../odbc/reference/develop-app/block-cursors.md) y [los cursores desplazables](../../../odbc/reference/develop-app/scrollable-cursors.md). Para obtener información acerca de la actualización, eliminación e inserción de filas, vea [Introducción a la actualización datos](../../../odbc/reference/develop-app/updating-data-overview.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [¿Era un conjunto creado de resultados?](../../../odbc/reference/develop-app/was-a-result-set-created.md)  
  
-   [Metadatos del conjunto de resultados](../../../odbc/reference/develop-app/result-set-metadata.md)  
  
-   [Enlazar columnas](../../../odbc/reference/develop-app/binding-columns.md)  
  
-   [Obtener datos](../../../odbc/reference/develop-app/fetching-data.md)  
  
-   [Cierre el Cursor](../../../odbc/reference/develop-app/closing-the-cursor.md)
