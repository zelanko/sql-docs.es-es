---
description: Al recuperar los resultados (Basic)
title: Recuperando resultados (Basic) | Microsoft Docs
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
ms.openlocfilehash: a43064703e7ee448de89396135fa610e972e2679
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461367"
---
# <a name="retrieving-results-basic"></a>Al recuperar los resultados (Basic)
Un *conjunto de resultados* es un conjunto de filas del origen de datos que coincide con determinados criterios. Se trata de una tabla conceptual que resulta de una consulta y que está disponible para una aplicación en formato tabular. Las instrucciones **Select** , las funciones de catálogo y algunos procedimientos crean conjuntos de resultados. En el ejemplo siguiente, la primera instrucción SQL crea un conjunto de resultados que contiene todas las filas y todas las columnas de la tabla Orders, y la segunda instrucción SQL crea un conjunto de resultados que contiene las columnas OrderID, SalesPerson y status para las filas de la tabla Orders en las que el estado es OPEN:  
  
```  
SELECT * FROM Orders  
SELECT OrderID, SalesPerson, Status FROM Orders WHERE Status = 'OPEN'  
```  
  
 Un conjunto de resultados puede estar vacío, que es diferente de ningún conjunto de resultados. Por ejemplo, la siguiente instrucción SQL crea un conjunto de resultados vacío:  
  
```  
SELECT * FROM Orders WHERE 1 = 2  
```  
  
 Un conjunto de resultados vacío no es diferente de ningún otro conjunto de resultados, salvo que no tiene ninguna fila. Por ejemplo, la aplicación puede recuperar metadatos para el conjunto de resultados, puede intentar capturar filas y debe cerrar el cursor sobre el conjunto de resultados.  
  
 El proceso de recuperar filas del origen de datos y devolverlas a la aplicación se denomina *captura*. En esta sección se explican las partes básicas de ese proceso. Para obtener información sobre temas más avanzados, como cursores de bloque y desplazables, consulte cursores de [bloque](../../../odbc/reference/develop-app/block-cursors.md) y [cursores desplazables](../../../odbc/reference/develop-app/scrollable-cursors.md). Para obtener información sobre cómo actualizar, eliminar e insertar filas, vea [información general](../../../odbc/reference/develop-app/updating-data-overview.md)sobre la actualización de datos.  
  
 Esta sección contiene los temas siguientes.  
  
-   [¿Era un conjunto creado de resultados?](../../../odbc/reference/develop-app/was-a-result-set-created.md)  
  
-   [Metadatos del conjunto de resultados](../../../odbc/reference/develop-app/result-set-metadata.md)  
  
-   [Enlazar columnas](../../../odbc/reference/develop-app/binding-columns.md)  
  
-   [Capturando datos](../../../odbc/reference/develop-app/fetching-data.md)  
  
-   [Cierre el Cursor](../../../odbc/reference/develop-app/closing-the-cursor.md)
