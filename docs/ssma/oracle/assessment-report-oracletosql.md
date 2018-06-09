---
title: Informe de evaluación (OracleToSQL) | Documentos de Microsoft
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
ms.openlocfilehash: aeba85eece49f126ac22f5f048e751f5bef16a15
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2018
ms.locfileid: "34777101"
---
# <a name="assessment-report-oracletosql"></a>Informe de evaluación (OracleToSQL)
Los resultados de la conversión de objetos de base de datos que muestra la ventana de informe de evaluación [!INCLUDE[tsql](../../includes/tsql_md.md)] sintaxis, y también puede ayudarle a calcular la complejidad y el costo de los proyectos de migración.  
  
Para obtener acceso al informe de evaluación, seleccionar objetos para convertir en el Explorador de metadatos de origen, haga clic en **esquemas** o **sinónimos**y, a continuación, seleccione **crear informe**.  
  
## <a name="options"></a>Opciones  
  
|||  
|-|-|  
|Término|Definición|  
|**Estadísticas de conversión**|Muestra las estadísticas de la conversión al tipo de instrucción. Este panel está visible cuando un objeto de grupo, como un esquema, o se selecciona un objeto sin código en el panel izquierdo.|  
|**Objetos por categorías**|Muestra el número de objetos por categoría. Este panel está visible cuando un objeto de grupo, como un esquema, o se selecciona un objeto sin código en el panel izquierdo.|  
|**Estadísticas**|Muestra las estadísticas de conversión para el objeto seleccionado. Este panel sólo es visible cuando se selecciona un objeto individual con el código en el panel izquierdo. Es posible que tengas que expandir **estadísticas**, que está inmediatamente por encima de la **origen** panel para ver este panel.|  
|**Source**|Muestra el código de Oracle para el objeto seleccionado y resalta código que no se ha convertido a [!INCLUDE[tsql](../../includes/tsql_md.md)]. Este panel sólo es visible cuando se selecciona un objeto individual con el código en el panel izquierdo.<br /><br />Haga clic en los números de línea para establecer o borrar marcadores. Utilice los botones en la parte superior del panel para navegar por el código.|  
|**Destino**|Muestra la conversión del resultante [!INCLUDE[tsql](../../includes/tsql_md.md)] código para el objeto seleccionado y los mensajes de error para el código que no se ha convertido. Este panel sólo es visible cuando se selecciona un objeto individual con el código en el panel izquierdo.<br /><br />Haga clic en los números de línea para establecer o borrar marcadores. Utilice los botones en la parte superior del panel para navegar por el código.|  
|**Panel mensajes**|Muestra los errores, advertencias y mensajes informativos que se generaron al crear el informe de evaluación. Los mensajes se agrupan por número. Para ver el código que produjo el error, haga clic en **errores**, **advertencias**, o **información**, expanda la categoría de mensajes y, a continuación, haga clic en un mensaje.|  
  
