---
title: "Advanced selección de objetos (DB2ToSQL) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: ca098c15-c343-4d7d-a284-c2fc405eb991
caps.latest.revision: "4"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d5f229e73487aab0be1f118c535f9d43851b44c7
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="advanced-object-selection-db2tosql"></a>Selección avanzada de objetos (DB2ToSQL)
El **sección avanzada de problemas de objeto** cuadro de diálogo permite filtrar los objetos de base de datos mediante el uso de cadenas y subcadenas en el nombre de objeto y, a continuación, seleccione o anule la selección de esos objetos. SSMA realiza operaciones de conversión y la migración en los objetos seleccionados.  
  
Para obtener acceso a este cuadro de diálogo, haga clic en el Explorador de metadatos y, a continuación, seleccione **selección avanzada de objeto**.  
  
Cuando abra por primera vez el cuadro de diálogo, haga clic en **mostrar elementos de subcategorías** para mostrar todos los objetos que tienen metadatos cargado en el proyecto. A continuación, puede escribir cadenas para filtrar los elementos. Por ejemplo, escriba la cadena "empresa" para mostrar todos los elementos con nombres que contengan esa cadena.  
  
Antes de utilizar este cuadro de diálogo, puede forzar SSMA para cargar todos los metadatos por convertir esquemas o guardar el proyecto.  
  
## <a name="options"></a>Opciones  
**Compruebe todos los elementos**  
Agrega una marca de verificación junto a todos los elementos. Estos elementos se seleccionará inmediatamente en el Explorador de metadatos.  
  
**Desactive todos los elementos**  
Quita la marca de verificación junto a todos los elementos. Estos elementos se borrará inmediatamente en el Explorador de metadatos.  
  
**Modo de vista de lista**  
Muestra elementos filtrados en una lista.  
  
**Modo de vista de tabla**  
Muestra elementos filtrados en una tabla.  
  
**Muestra elementos solo cargados**  
Alterna la presentación de categorías o elementos. Cuando se selecciona este botón, SSMA muestra todos los elementos que coinciden con los criterios de filtro y las que se haya cargado anteriormente. Cuando no se selecciona este botón, SSMA muestra las carpetas de categoría.  
  
**Filter**  
Escriba la cadena que desea usar para filtrar elementos. Por ejemplo, para buscar disponibles todos los elementos que contengan la cadena "Id." en el nombre del elemento, escriba la cadena "ID" en la **filtro** cuadro.  
  
Si los elementos que coincidan con los criterios de filtro, se mostrarán las categorías o los elementos a medida que escribe la cadena. Para ver los elementos coincidentes, se recomienda que haga clic en el **muestra solo los elementos cargados** botón.  
  
**Borrar filtro**  
Borra la **filtro** cuadro.  
  
