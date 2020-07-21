---
title: Informe de evaluación (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: af24f2c4-5e86-4135-a4f3-a24faaeeefe7
author: Shamikg
ms.author: Shamikg
ms.openlocfilehash: c6d83e81253430f243fcaed55b66f6d0de6299ca
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68083504"
---
# <a name="assessment-report-sybasetosql"></a>Informe de evaluación (SybaseToSQL)
La ventana Informe de evaluación muestra los resultados de la conversión de objetos de [!INCLUDE[tsql](../../includes/tsql-md.md)] base de datos a sintaxis y también puede ayudarle a calcular la complejidad y el costo de los proyectos de migración.  
  
Para tener acceso al informe de evaluación, seleccione los objetos que desea convertir en el explorador de metadatos de origen, haga clic con el botón derecho en **bases**de datos y, a continuación, seleccione **crear informe**.  
  
## <a name="options"></a>Opciones  
**Estadísticas de conversión**  
Muestra las estadísticas de conversión por tipo de instrucción. Este panel solo es visible cuando se selecciona un objeto de grupo, como un esquema, o un objeto sin código en el panel izquierdo.  
  
**Objetos por categoría**  
Muestra las estadísticas de conversión por tipo de objeto. Este panel solo es visible cuando se selecciona un objeto de grupo, como un esquema, o un objeto sin código en el panel izquierdo.  
  
**estadísticas**  
Muestra las estadísticas de conversión del objeto seleccionado. Este panel solo es visible cuando se selecciona un objeto individual con código en el panel izquierdo. Es posible que tenga que expandir las **estadísticas** para ver este panel.  
  
**Navegación de origen**  
Muestra el código de ASE para el objeto seleccionado y resalta el código que no se [!INCLUDE[tsql](../../includes/tsql-md.md)]convirtió en. Este panel solo es visible cuando se selecciona un objeto individual con código en el panel izquierdo.  
  
Haga clic en los números de línea para establecer o Borrar marcadores. Use los botones situados en la parte superior del panel para navegar por el código.  
  
**Navegación de destino**  
Muestra el código resultante [!INCLUDE[tsql](../../includes/tsql-md.md)] de la conversión para el objeto seleccionado y los mensajes de error para el código que no se ha convertido. Este panel solo es visible cuando se selecciona un objeto individual con código en el panel izquierdo.  
  
Haga clic en los números de línea para establecer o Borrar marcadores. Use los botones situados en la parte superior del panel para navegar por el código.  
  
**Panel Mensajes**  
Muestra los errores, las advertencias y los mensajes de información que se generan al crear el informe de evaluación. Los mensajes se agrupan por número. Para ver el código que causó el error, haga clic en **error**, **ADVERTENCIA**o **información**, expanda la categoría de mensajes y, a continuación, haga clic en un mensaje.  
  
