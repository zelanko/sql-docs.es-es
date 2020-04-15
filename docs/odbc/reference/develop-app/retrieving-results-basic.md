---
title: Recuperación de resultados (básico) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3f7d01bf92fcee07940e449a2fb4bbac4f0fe6ac
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304336"
---
# <a name="retrieving-results-basic"></a>Al recuperar los resultados (Basic)
Un conjunto de *resultados* es un conjunto de filas en el origen de datos que coincide con determinados criterios. Es una tabla conceptual que resulta de una consulta y que está disponible para una aplicación en forma tabular. Las instrucciones **SELECT,** las funciones de catálogo y algunos procedimientos crean conjuntos de resultados. En el ejemplo siguiente, la primera instrucción SQL crea un conjunto de resultados que contiene todas las filas y todas las columnas de la tabla Orders, y la segunda instrucción SQL crea un conjunto de resultados que contiene las columnas OrderID, SalesPerson y Status para las filas de la tabla Orders en la que Status es OPEN:  
  
```  
SELECT * FROM Orders  
SELECT OrderID, SalesPerson, Status FROM Orders WHERE Status = 'OPEN'  
```  
  
 Un conjunto de resultados puede estar vacío, lo que es diferente de ningún conjunto de resultados en absoluto. Por ejemplo, la siguiente instrucción SQL crea un conjunto de resultados vacío:  
  
```  
SELECT * FROM Orders WHERE 1 = 2  
```  
  
 Un conjunto de resultados vacío no es diferente de cualquier otro conjunto de resultados, excepto que no tiene filas. Por ejemplo, la aplicación puede recuperar metadatos para el conjunto de resultados, puede intentar capturar filas y debe cerrar el cursor sobre el conjunto de resultados.  
  
 El proceso de recuperar filas del origen de datos y devolverlas a la aplicación se denomina *obtención*. En esta sección se explican las partes básicas de ese proceso. Para obtener información sobre temas más avanzados, como cursores de bloque y desplazables, vea [Cursores](../../../odbc/reference/develop-app/block-cursors.md) de bloque y [Cursores desplazables](../../../odbc/reference/develop-app/scrollable-cursors.md). Para obtener información sobre cómo actualizar, eliminar e insertar filas, consulte Actualización de información [general de datos](../../../odbc/reference/develop-app/updating-data-overview.md).  
  
 Esta sección contiene los temas siguientes.  
  
-   [¿Era un conjunto creado de resultados?](../../../odbc/reference/develop-app/was-a-result-set-created.md)  
  
-   [Metadatos del conjunto de resultados](../../../odbc/reference/develop-app/result-set-metadata.md)  
  
-   [Enlazar columnas](../../../odbc/reference/develop-app/binding-columns.md)  
  
-   [Obtener datos](../../../odbc/reference/develop-app/fetching-data.md)  
  
-   [Cierre el Cursor](../../../odbc/reference/develop-app/closing-the-cursor.md)
