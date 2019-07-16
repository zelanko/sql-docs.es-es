---
title: Informe de evaluación (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 9e13eba0-e3cf-4205-974f-c00f982061de
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: 017bb1a123c7465efd7ad895bb34fec8b87a707e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938306"
---
# <a name="assessment-report-db2tosql"></a>Informe de evaluación (DB2ToSQL)
La ventana Informe de evaluación muestra los resultados de la conversión de objetos de base de datos a [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxis, y también puede ayudarle a estimar la complejidad y el costo de los proyectos de migración.  
  
Para tener acceso al informe de evaluación, seleccionar objetos para convertir en el Explorador de metadatos de origen, haga clic en **esquemas** o **sinónimos**y, a continuación, seleccione **crear informe**.  
  
## <a name="options"></a>Opciones  
  
|||  
|-|-|  
|Término|Definición|  
|**Estadísticas de conversión**|Muestra las estadísticas de la conversión al tipo de instrucción. Este panel está visible cuando un objeto de grupo, como un esquema, o se selecciona un objeto sin código en el panel izquierdo.|  
|**Objetos por categorías**|Muestra el número de objetos por categoría. Este panel está visible solo cuando un objeto de grupo, como un esquema, o se selecciona un objeto sin código en el panel izquierdo.|  
|**Estadísticas**|Muestra las estadísticas de conversión para el objeto seleccionado. Este panel está visible solo cuando se selecciona un objeto individual con el código en el panel izquierdo. Es posible que deba expandir **estadísticas**, que está inmediatamente por encima del **origen** panel para ver este panel.|  
|**Origen**|Muestra el código de DB2 para el objeto seleccionado y resalta el código que no se ha convertido a [!INCLUDE[tsql](../../includes/tsql-md.md)]. Este panel está visible solo cuando se selecciona un objeto individual con el código en el panel izquierdo.<br /><br />Haga clic en los números de línea para establecer o borrar marcadores. Utilice los botones en la parte superior del panel para navegar por el código.|  
|**Destino**|Se muestra la conversión del resultante [!INCLUDE[tsql](../../includes/tsql-md.md)] código para el objeto seleccionado y los mensajes de error para el código que no se ha convertido. Este panel está visible solo cuando se selecciona un objeto individual con el código en el panel izquierdo.<br /><br />Haga clic en los números de línea para establecer o borrar marcadores. Utilice los botones en la parte superior del panel para navegar por el código.|  
|**Panel de mensajes**|Muestra los errores, advertencias y mensajes informativos que se generaron al crear el informe de evaluación. Los mensajes se agrupan por número. Para ver el código que produjo el error, haga clic en **errores**, **advertencias**, o **información**, expanda la categoría de mensajes y, a continuación, haga clic en un mensaje.|  
  
