---
description: Selección avanzada de objetos (AccessToSQL)
title: Selección avanzada de objetos (AccessToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 4d2b367f-8ac7-4534-b66f-10300ef64ebc
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 0b5dfe862f48b2669d0535066fe36e4a892c5dfa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88418591"
---
# <a name="advanced-object-selection--accesstosql"></a>Selección avanzada de objetos (AccessToSQL)
El cuadro de diálogo **sección de objeto avanzado** permite filtrar los objetos de base de datos mediante cadenas y subcadenas en el nombre del objeto y, a continuación, seleccionar o anular la selección de esos objetos. SSMA realiza operaciones de conversión y migración en objetos seleccionados.  
  
Para obtener acceso a este cuadro de diálogo, haga clic con el botón derecho en un explorador de metadatos y seleccione **selección avanzada de objetos**.  
  
Cuando abra por primera vez el cuadro de diálogo, haga clic en **Mostrar elementos de subcategorías** para mostrar todos los objetos que tienen metadatos cargados en el proyecto. Después, puede escribir cadenas para filtrar los elementos. Por ejemplo, escriba la cadena "Company" para mostrar todos los elementos cuyos nombres incluyan esa cadena.  
  
Antes de utilizar este cuadro de diálogo, puede forzar a SSMA para cargar todos los metadatos, ya sea convirtiendo los esquemas o guardando el proyecto.  
  
## <a name="options"></a>Opciones  
**Comprobar todos los elementos**  
Agrega una marca de verificación junto a todos los elementos. Estos elementos se seleccionarán inmediatamente en el explorador de metadatos.  
  
**Desactivar todos los elementos**  
Quita la marca de verificación junto a todos los elementos. Estos elementos se borrarán inmediatamente en el explorador de metadatos.  
  
**Modo de vista de lista**  
Muestra los elementos filtrados en una lista.  
  
**Modo de vista de tabla**  
Muestra los elementos filtrados en una tabla.  
  
**Solo se muestran los elementos cargados**  
Alterna la presentación de categorías o elementos. Cuando se selecciona este botón, SSMA muestra todos los elementos que coinciden con los criterios de filtro y los que se cargaron previamente. Cuando no se selecciona este botón, SSMA muestra las carpetas de categorías.  
  
**Filter**  
Escriba la cadena que desea utilizar para filtrar elementos. Por ejemplo, para buscar todos los elementos disponibles que contengan la cadena "ID" en el nombre del elemento, escriba la cadena "ID" en el cuadro de **filtro** .  
  
Si los elementos coinciden con los criterios de filtro, las categorías o elementos aparecerán a medida que se escribe la cadena. Para ver los elementos coincidentes, se recomienda hacer clic en el botón **solo elementos cargados mostrados** .  
  
**Borrar filtro**  
Borra el cuadro de **filtro** .  
  
