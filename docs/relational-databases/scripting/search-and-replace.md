---
title: Buscar y reemplazar | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b0a9da8a3a49bad8d24e663b2d49fda596c0127a
ms.sourcegitcommit: a0aa5e611a0e6ebb74ac1e2f613e8916dc7a7617
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/24/2018
---
# <a name="search-and-replace"></a>Buscar y reemplazar
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Existen varias maneras de buscar y reemplazar texto. En el menú **Editar** , **Buscar y reemplazar** ofrece cuatro opciones: **Búsqueda rápida**, **Reemplazo rápido**, **Buscar en archivos**o **Reemplazar en archivos**. Cada una abre versiones del cuadro de diálogo **Buscar y reemplazar** . También es posible buscar sin un cuadro de diálogo mediante los métodos abreviados de teclado para búsqueda incremental. Estas técnicas permiten controlar el ámbito de búsqueda y reemplazo y elegir el método de revisión de las coincidencias de búsqueda y los reemplazos.  
  
 A la hora de buscar y reemplazar texto, es necesario tener en cuenta lo siguiente:  
  
-   Las opciones establecidas en el cuadro de diálogo **Buscar y reemplazar** afectan a todas las búsquedas. Estas opciones incluyen **Coincidir mayúsculas y minúsculas**, **Solo palabras completas**, **Buscar hacia atrás**, **Buscar en texto oculto**, **Usar Caracteres comodín**, **Usar Expresiones regulares**, **Buscar en Todos los documentos abiertos**y **Buscar en Proyecto actual**. Todas las opciones no están disponibles en todas las versiones del cuadro de diálogo **Buscar y reemplazar** .  
  
-   **Deshacer** solo está disponible para aquellos documentos que se dejan abiertos tras una operación de reemplazo.  
  
-   **Deshacer** para una operación **Reemplazar todo** que abarca más de un archivo se considera una acción única masiva en todos los archivos afectados. Es decir, no es posible deshacer el cambio en algunos archivos y no en otros.  
  
 Normalmente no es posible buscar elementos mediante vistas gráficas.  
  
## <a name="see-also"></a>Ver también  
 [Buscar en un documento activo de forma incremental](../../relational-databases/scripting/search-an-active-document-incrementally.md)   
 [Buscar documentos de forma interactiva](../../relational-databases/scripting/search-documents-interactively.md)   
 [Buscar en documentos mediante las listas de resultados](../../relational-databases/scripting/search-documents-using-results-lists.md)   
 [Buscar texto con caracteres comodín](../../relational-databases/scripting/search-text-with-wildcards.md)   
 [Buscar texto mediante expresiones regulares](../../relational-databases/scripting/search-text-with-regular-expressions.md)  
  
  
