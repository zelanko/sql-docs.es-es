---
title: Selección avanzada de objetos (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.technology: ssma
ms.topic: conceptual
ms.assetid: d2baa90f-1b77-47ce-988d-1910c7c74103
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 2f1ee73e2d6ad21ea57825bd31997db0a519a720
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63283621"
---
# <a name="advanced-object-selection-sybasetosql"></a>Selección avanzada de objetos (SybaseToSQL)
El **avanzada objeto sección** cuadro de diálogo le permite filtrar los objetos de base de datos mediante el uso de cadenas y las subcadenas en el nombre del objeto y, a continuación, seleccione o anule la selección de esos objetos. SSMA realiza operaciones de conversión y la migración en los objetos seleccionados.  
  
Para acceder a este cuadro de diálogo, haga clic en un explorador de metadatos y, a continuación, seleccione **selección avanzada de objeto**.  
  
Al abrir el cuadro de diálogo, haga clic en **mostrar elementos de subcategorías** para mostrar todos los objetos que tienen los metadatos que se cargan en el proyecto. A continuación, puede escribir cadenas para filtrar los elementos. Por ejemplo, escriba la cadena "company" Mostrar todos los elementos con nombres que contengan esa cadena.  
  
Antes de utilizar este cuadro de diálogo, puede forzar SSMA para cargar todos los metadatos de conversión de esquemas o guardar el proyecto.  
  
## <a name="options"></a>Opciones  
**Compruebe todos los elementos**  
Agrega una marca de verificación junto a todos los elementos. Estos elementos se seleccionará inmediatamente en el Explorador de metadatos.  
  
**Desactive todos los elementos**  
Quita la marca de verificación junto a todos los elementos. Estos elementos se borrará inmediatamente en el Explorador de metadatos.  
  
**Modo de vista de lista**  
Muestra elementos filtrados en una lista.  
  
**Modo de vista de tabla**  
Muestra elementos filtrados en una tabla.  
  
**Mostrar elementos sólo cargados**  
Alterna la visualización de categorías o elementos. Cuando se selecciona este botón, SSMA muestra todos los elementos que coinciden con los criterios de filtro y los que se cargaron previamente. Cuando no se selecciona este botón, SSMA muestra las carpetas de categoría.  
  
**Filter**  
Escriba la cadena que desea usar para filtrar los elementos. Por ejemplo, para buscar los elementos disponibles que contienen la cadena "Id." en el nombre del elemento, escriba la cadena "ID" en el **filtro** cuadro.  
  
Si los elementos que coincidan con los criterios de filtro, aparecerán las categorías o elementos a medida que escribe la cadena. Para ver los elementos que coinciden, se recomienda que haga clic en el **muestra sólo los elementos cargados** botón.  
  
**Borrar filtro**  
Borra la **filtro** cuadro.  
  
