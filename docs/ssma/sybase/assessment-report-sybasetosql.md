---
title: Informe de evaluación (SybaseToSQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssma-sybase
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: af24f2c4-5e86-4135-a4f3-a24faaeeefe7
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 777fab9d35118b4cffab8ed8f947a4e91cb2480d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="assessment-report-sybasetosql"></a>Informe de evaluación (SybaseToSQL)
Los resultados de la conversión de objetos de base de datos que muestra la ventana de informe de evaluación [!INCLUDE[tsql](../../includes/tsql_md.md)] sintaxis, y también puede ayudarle a calcular la complejidad y el costo de los proyectos de migración.  
  
Para obtener acceso al informe de evaluación, seleccionar objetos para convertir en el Explorador de metadatos de origen, haga clic en **bases de datos**y, a continuación, seleccione **crear informe**.  
  
## <a name="options"></a>Opciones  
**Estadísticas de conversión**  
Muestra las estadísticas de la conversión al tipo de instrucción. Este panel está visible cuando un objeto de grupo, como un esquema, o se selecciona un objeto sin código en el panel izquierdo.  
  
**Objetos por categoría**  
Muestra las estadísticas de la conversión al tipo de objeto. Este panel está visible cuando un objeto de grupo, como un esquema, o se selecciona un objeto sin código en el panel izquierdo.  
  
**Estadísticas**  
Muestra las estadísticas de conversión para el objeto seleccionado. Este panel sólo es visible cuando se selecciona un objeto individual con el código en el panel izquierdo. Es posible que tengas que expandir **estadísticas** para ver este panel.  
  
**Navegación de origen**  
Muestra el código de ASE para el objeto seleccionado y resalta código que no se ha convertido a [!INCLUDE[tsql](../../includes/tsql_md.md)]. Este panel sólo es visible cuando se selecciona un objeto individual con el código en el panel izquierdo.  
  
Haga clic en los números de línea para establecer o borrar marcadores. Utilice los botones en la parte superior del panel para navegar por el código.  
  
**Navegación de destino**  
Muestra la conversión del resultante [!INCLUDE[tsql](../../includes/tsql_md.md)] código para el objeto seleccionado y los mensajes de error para el código que no se ha convertido. Este panel sólo es visible cuando se selecciona un objeto individual con el código en el panel izquierdo.  
  
Haga clic en los números de línea para establecer o borrar marcadores. Utilice los botones en la parte superior del panel para navegar por el código.  
  
**Panel mensajes**  
Muestra los errores, advertencias y mensajes informativos que se generan al crear el informe de evaluación. Los mensajes se agrupan por número. Para ver el código que produjo el error, haga clic en **Error**, **advertencia**, o **información**, expanda la categoría de mensajes y, a continuación, haga clic en un mensaje.  
  
