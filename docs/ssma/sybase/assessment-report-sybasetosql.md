---
title: Informe de evaluación (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: af24f2c4-5e86-4135-a4f3-a24faaeeefe7
author: nahk-ivanov
ms.author: alexiva
ms.openlocfilehash: 11b47065fe180956d58361ec80eda1dac25fa4b1
ms.sourcegitcommit: e8f6c51d4702c0046aec1394109bc0503ca182f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/07/2020
ms.locfileid: "87932326"
---
# <a name="assessment-report-sybasetosql"></a>Informe de evaluación (SybaseToSQL)
La ventana Informe de evaluación muestra los resultados de la conversión de objetos de base de datos a [!INCLUDE[tsql](../../includes/tsql-md.md)] sintaxis y también puede ayudarle a calcular la complejidad y el costo de los proyectos de migración.  
  
Para tener acceso al informe de evaluación, seleccione los objetos que desea convertir en el explorador de metadatos de origen, haga clic con el botón derecho en **bases**de datos y, a continuación, seleccione **crear informe**.  
  
## <a name="options"></a>Opciones  
**Estadísticas de conversión**  
Muestra las estadísticas de conversión por tipo de instrucción. Este panel solo es visible cuando se selecciona un objeto de grupo, como un esquema, o un objeto sin código en el panel izquierdo.  
  
**Objetos por categoría**  
Muestra las estadísticas de conversión por tipo de objeto. Este panel solo es visible cuando se selecciona un objeto de grupo, como un esquema, o un objeto sin código en el panel izquierdo.  
  
**estadísticas**  
Muestra las estadísticas de conversión del objeto seleccionado. Este panel solo es visible cuando se selecciona un objeto individual con código en el panel izquierdo. Es posible que tenga que expandir las **estadísticas** para ver este panel.  
  
**Navegación de origen**  
Muestra el código de ASE para el objeto seleccionado y resalta el código que no se convirtió en [!INCLUDE[tsql](../../includes/tsql-md.md)] . Este panel solo es visible cuando se selecciona un objeto individual con código en el panel izquierdo.  
  
Haga clic en los números de línea para establecer o Borrar marcadores. Use los botones situados en la parte superior del panel para navegar por el código.  
  
**Navegación de destino**  
Muestra el código resultante de [!INCLUDE[tsql](../../includes/tsql-md.md)] la conversión para el objeto seleccionado y los mensajes de error para el código que no se ha convertido. Este panel solo es visible cuando se selecciona un objeto individual con código en el panel izquierdo.  
  
Haga clic en los números de línea para establecer o Borrar marcadores. Use los botones situados en la parte superior del panel para navegar por el código.  
  
**Panel Mensajes**  
Muestra los errores, las advertencias y los mensajes de información que se generan al crear el informe de evaluación. Los mensajes se agrupan por número. Para ver el código que causó el error, haga clic en **error**, **ADVERTENCIA**o **información**, expanda la categoría de mensajes y, a continuación, haga clic en un mensaje.  
  
