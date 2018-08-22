---
title: Informe de evaluación (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 9e13eba0-e3cf-4205-974f-c00f982061de
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: b8217aa8346afd27ceba71b4cc929597e74dee9d
ms.sourcegitcommit: b70b99c2e412b4d697021f3bf1a92046aafcbe37
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/13/2018
ms.locfileid: "40396339"
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
|**Source**|Muestra el código de DB2 para el objeto seleccionado y resalta el código que no se ha convertido a [!INCLUDE[tsql](../../includes/tsql-md.md)]. Este panel está visible solo cuando se selecciona un objeto individual con el código en el panel izquierdo.<br /><br />Haga clic en los números de línea para establecer o borrar marcadores. Utilice los botones en la parte superior del panel para navegar por el código.|  
|**Destino**|Se muestra la conversión del resultante [!INCLUDE[tsql](../../includes/tsql-md.md)] código para el objeto seleccionado y los mensajes de error para el código que no se ha convertido. Este panel está visible solo cuando se selecciona un objeto individual con el código en el panel izquierdo.<br /><br />Haga clic en los números de línea para establecer o borrar marcadores. Utilice los botones en la parte superior del panel para navegar por el código.|  
|**Panel de mensajes**|Muestra los errores, advertencias y mensajes informativos que se generaron al crear el informe de evaluación. Los mensajes se agrupan por número. Para ver el código que produjo el error, haga clic en **errores**, **advertencias**, o **información**, expanda la categoría de mensajes y, a continuación, haga clic en un mensaje.|  
  
