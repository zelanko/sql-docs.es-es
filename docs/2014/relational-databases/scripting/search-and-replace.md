---
title: Buscar y reemplazar | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- match case [SQL Server]
- undo operations
- searches [SQL Server Management Studio]
- replacing text
- quick search and replaces [SQL Server Management Studio]
- Query Editor [SQL Server Management Studio], undo
- Query Editor [SQL Server Management Studio], searching
- regular expressions [SQL Server Management Studio]
- finding text [SQL Server Management Studio]
- text [SQL Server], search and replace operations
- finding [SQL Server Management Studio]
- locating text
- Query Editor [SQL Server Management Studio], replacing text
- Find and Replace dialog box
- wildcard options [SQL Server Management Studio]
- match whole word [SQL Server]
- searches [SQL Server Management Studio], replacing
ms.assetid: 3641c7b3-3e3e-4ddd-af82-c15b50004f94
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cce96567d465c4b0c10741ac8a10b08902405368
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66090202"
---
# <a name="search-and-replace"></a>Buscar y reemplazar
  Existen varias maneras de buscar y reemplazar texto. En el **editar** menú, **buscar y reemplazar** ofrece cuatro opciones: **Búsqueda rápida**, **reemplazo rápido**, **buscar en archivos**, o **reemplazar en archivos**. Cada una abre versiones del cuadro de diálogo **Buscar y reemplazar** . También es posible buscar sin un cuadro de diálogo mediante los métodos abreviados de teclado para búsqueda incremental. Estas técnicas permiten controlar el ámbito de búsqueda y reemplazo y elegir el método de revisión de las coincidencias de búsqueda y los reemplazos.  
  
 A la hora de buscar y reemplazar texto, es necesario tener en cuenta lo siguiente:  
  
-   Las opciones establecidas en el cuadro de diálogo **Buscar y reemplazar** afectan a todas las búsquedas. Estas opciones incluyen **Coincidir mayúsculas y minúsculas**, **Solo palabras completas**, **Buscar hacia atrás**, **Buscar en texto oculto**, **Usar Caracteres comodín**, **Usar Expresiones regulares**, **Buscar en Todos los documentos abiertos**y **Buscar en Proyecto actual**. Todas las opciones no están disponibles en todas las versiones del cuadro de diálogo **Buscar y reemplazar** .  
  
-   **Deshacer** solo está disponible para aquellos documentos que se dejan abiertos tras una operación de reemplazo.  
  
-   **Deshacer** para una operación **Reemplazar todo** que abarca más de un archivo se considera una acción única masiva en todos los archivos afectados. Es decir, no es posible deshacer el cambio en algunos archivos y no en otros.  
  
 Normalmente no es posible buscar elementos mediante vistas gráficas.  
  
## <a name="see-also"></a>Vea también  
 [Buscar en un documento activo de forma incremental](search-an-active-document-incrementally.md)   
 [Buscar documentos de forma interactiva](search-documents-interactively.md)   
 [Buscar en documentos mediante las listas de resultados](search-documents-using-results-lists.md)   
 [Buscar texto con caracteres comodín](search-text-with-wildcards.md)   
 [Buscar texto mediante expresiones regulares](search-text-with-regular-expressions.md)  
  
  
