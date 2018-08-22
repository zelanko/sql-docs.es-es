---
title: Informe de evaluación (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 168b7465-a6d6-4329-b46e-fc6c5a3f2d9d
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 2dd0a63d9637a44f387c3e3f862387a8c4866d18
ms.sourcegitcommit: b70b99c2e412b4d697021f3bf1a92046aafcbe37
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/13/2018
ms.locfileid: "40394916"
---
# <a name="assessment-report-oracletosql"></a>Informe de evaluación (OracleToSQL)
La ventana Informe de evaluación muestra los resultados de la conversión de objetos de base de datos a [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxis, y también puede ayudarle a estimar la complejidad y el costo de los proyectos de migración.  
  
Para tener acceso al informe de evaluación, seleccionar objetos para convertir en el Explorador de metadatos de origen, haga clic en **esquemas** o **sinónimos**y, a continuación, seleccione **crear informe**.  
  
## <a name="options"></a>Opciones  
  
|||  
|-|-|  
|Término|Definición|  
|**Estadísticas de conversión**|Muestra las estadísticas de la conversión al tipo de instrucción. Este panel está visible cuando un objeto de grupo, como un esquema, o se selecciona un objeto sin código en el panel izquierdo.|  
|**Objetos por categorías**|Muestra el número de objetos por categoría. Este panel está visible solo cuando un objeto de grupo, como un esquema, o se selecciona un objeto sin código en el panel izquierdo.|  
|**Estadísticas**|Muestra las estadísticas de conversión para el objeto seleccionado. Este panel está visible solo cuando se selecciona un objeto individual con el código en el panel izquierdo. Es posible que deba expandir **estadísticas**, que está inmediatamente por encima del **origen** panel para ver este panel.|  
|**Source**|Muestra el código de Oracle para el objeto seleccionado y resalta el código que no se ha convertido a [!INCLUDE[tsql](../../includes/tsql-md.md)]. Este panel está visible solo cuando se selecciona un objeto individual con el código en el panel izquierdo.<br /><br />Haga clic en los números de línea para establecer o borrar marcadores. Utilice los botones en la parte superior del panel para navegar por el código.|  
|**Destino**|Se muestra la conversión del resultante [!INCLUDE[tsql](../../includes/tsql-md.md)] código para el objeto seleccionado y los mensajes de error para el código que no se ha convertido. Este panel está visible solo cuando se selecciona un objeto individual con el código en el panel izquierdo.<br /><br />Haga clic en los números de línea para establecer o borrar marcadores. Utilice los botones en la parte superior del panel para navegar por el código.|  
|**Panel de mensajes**|Muestra los errores, advertencias y mensajes informativos que se generaron al crear el informe de evaluación. Los mensajes se agrupan por número. Para ver el código que produjo el error, haga clic en **errores**, **advertencias**, o **información**, expanda la categoría de mensajes y, a continuación, haga clic en un mensaje.|  
  
