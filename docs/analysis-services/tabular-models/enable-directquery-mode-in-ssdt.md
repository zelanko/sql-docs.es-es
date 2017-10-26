---
title: Habilitar el modo DirectQuery en SSDT | Documentos de Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 07/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 71fc7ebd-2e86-4a76-994b-66d3a57bcc9b
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9f3a5cfe3f2b39f35d2b2e70dd44ec11adeebcd0
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="enable-directquery-mode-in-ssdt"></a>Habilitar el modo DirectQuery en SSDT

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

En este tema se describe cómo habilitar el modo DirectQuery para un proyecto de modelo tabular en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)].  
  
Cuando se habilita el modo DirectQuery para un modelo tabular que se está diseñando en SSDT:
-   Las características que sean incompatibles con el modo DirectQuery se deshabilitarán.  
-   El modelo existente se validará. Se mostrarán advertencias si hay características incompatibles con el modo DirectQuery.  
-   Si se importaron datos antes de habilitar el modo DirectQuery, se vaciará la memoria caché del modelo de trabajo.  
  
### <a name="enable-directquery"></a>Habilitar DirectQuery  
  
En SSDT, en el panel **Propiedades** del archivo **Model.bim** , cambie la propiedad **Modo DirectQuery**a **Activado**.  

![Habilitar el modo DirectQuery en SSDT](../../analysis-services/tabular-models/media/enable-directquery-mode-in-ssdt.png)
  
Si el modelo ya tiene una conexión con un origen de datos y los datos existentes, se solicitará que escriba las credenciales de base de datos usadas para conectarse a la base de datos relacional. Los datos existentes en el modelo se quitarán de la caché en memoria.  
  
Si el modelo está total o parcialmente completo, antes de habilitar el modo DirectQuery, podría obtener errores sobre características incompatibles. Abra la **Lista de errores** en Visual Studio y solucione los problemas que impiden que el modelo se cambie al modo DirectQuery.  


### <a name="whats-next"></a>¿Qué debe hacer a continuación? 
Ahora puede importar datos mediante el Asistente para la importación de tablas a fin de obtener metadatos para el modelo. No obtendrá filas de datos, pero sí tablas, columnas y relaciones que puede usar como base para el modelo. 

Puede crear una partición de ejemplo para cada tabla y agregar datos de ejemplo para poder comprobar el comportamiento del modelo a medida que lo genera. Los datos de ejemplo que agregue se usan en **Analyze for Excel** (Analizar para Excel) o en otras herramientas de cliente que pueden conectarse a la base de datos del área de trabajo. Vea [Agregar datos de ejemplo a un modelo de DirectQuery en el modo de diseño](../../analysis-services/tabular-models/add-sample-data-to-a-directquery-model-in-design-mode.md) para obtener más información.  
  
> [!TIP]  
    >  Incluso en el modo DirectQuery de un modelo vacío, siempre se puede ver un pequeño conjunto de filas integrado para cada tabla. En [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], haga clic en **Tabla** > **Propiedades de tabla** para ver el conjunto de datos de 50 filas.  
  
  
## <a name="see-also"></a>Vea también  
[Habilitar el modo DirectQuery en SSMS](../../analysis-services/tabular-models/enable-directquery-mode-in-ssms.md)

[Agregar datos de ejemplo a un modelo de DirectQuery en el modo de diseño](../../analysis-services/tabular-models/add-sample-data-to-a-directquery-model-in-design-mode.md)
  

