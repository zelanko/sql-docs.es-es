---
title: Usar SQL Server Profiler para supervisar la minería de datos (Analysis Services-minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Profiler [SQL Server Profiler], Analysis Services
ms.assetid: 655ac93c-5c5c-4565-914b-915327f7d349
author: minewiskan
ms.author: owend
ms.openlocfilehash: 136f81e374878a9af8241175f1519c87a266515f
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/08/2020
ms.locfileid: "84520186"
---
# <a name="using-sql-server-profiler-to-monitor-data-mining-analysis-services---data-mining"></a>Usar SQL Server Profiler para supervisar la minería de datos (Analysis Services - Minería de datos)
  Si dispone de los permisos necesarios, puede utilizar SQL Server Profiler para supervisar las actividades de minería de datos que se emiten como solicitudes que se envían a una instancia de SQL Server Analysis Services. La actividad de minería de datos puede incluir el procesamiento de modelos o estructuras, consultas de predicción o consultas de contenido, o la creación de nuevos modelos o estructuras.  
  
 SQL Server Profiler utiliza `trace` para supervisar las solicitudes enviadas desde varios clientes, como [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], SQL Server Management Studio, servicios web o los Complementos de minería de datos para Excel, siempre que todas las actividades usen la misma instancia de SQL Server Analysis Services. Debe crear un seguimiento independiente para cada instancia de SQL Server Analysis Services que desee supervisar. Para obtener información general sobre los seguimientos y cómo usar SQL Server Profiler, vea [Usar SQL Server Profiler para supervisar Analysis Services](../instances/use-sql-server-profiler-to-monitor-analysis-services.md).  
  
 Para obtener instrucciones específicas sobre los tipos de eventos que se capturan, vea [Crear seguimientos del generador de perfiles para su reproducción &#40;Analysis Services&#41;](../instances/create-profiler-traces-for-replay-analysis-services.md).  
  
## <a name="using-traces-to-monitor-data-mining"></a>Usar seguimientos para supervisar la minería de datos  
 Al capturar información en un seguimiento, puede especificar si se guarda en un archivo o en una tabla en una instancia de SQL Server. Independientemente del método que use para almacenar los datos, puede utilizar SQL Server Profiler para ver el seguimiento y filtrar por eventos. En la tabla siguiente se muestran algunos eventos y subclases del seguimiento predeterminado de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que tienen interés para la minería de datos.  
  
|EventClass|EventSubclass|Descripción|  
|----------------|-------------------|-----------------|  
|**Inicio de la consulta**<br /><br /> **Final de la consulta**|**0 - MDXQuery**|Contiene el texto de todas las llamadas a los procedimientos almacenados de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|**Inicio de la consulta**<br /><br /> **Final de la consulta**|**1 - DMXQuery**|Contiene el texto y los resultados de las instrucciones de Extensiones de minería de datos (DMX).|  
|**Progress Report Begin**<br /><br /> **Progress Report End**|**34 - DataMiningProgress**|Proporciona información sobre el progreso del algoritmo de minería de datos: por ejemplo, si está generando un modelo de agrupación en clústeres, el mensaje de progreso le indica qué clúster candidato se está generando.|  
|**Inicio de la consulta**<br /><br /> **Final de la consulta**|EXECUTESQL|Contiene el texto de la consulta de Transact-SQL que se ejecuta|  
|**Inicio de la consulta**<br /><br /> **Final de la consulta**|**2-SQLQuery**|Contiene el texto de cualquier consulta con los conjuntos de filas de esquema en formato de tablas del sistema.|  
|**Inicio de la detección**<br /><br /> **Fin de DISCOVER**|Múltiple|Contiene el texto de las llamadas a la función DMX o las instrucciones DISCOVER, encapsuladas en XMLA.|  
|**Error**|(ninguno)|Contiene el texto de los errores que el servidor envía al cliente.<br /><br /> Los mensajes de error precedidos de **Error (Minería de datos):** o **Informativo (Minería de datos):** se generan específicamente en respuesta a las solicitudes DMX. Sin embargo, no es suficiente ver solo estos mensajes de error. Otros errores, como los que genera el analizador, pueden estar relacionados con la minería de datos y no tener este prefijo.|  
  
 Al ver las instrucciones de comandos en el registro de seguimiento, también puede ver la sintaxis de las instrucciones complejas que el cliente envía al servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , incluidas las llamadas a los procedimientos almacenados del sistema. Esta información puede ser útil para depurar o puede utilizar las instrucciones válidas como plantilla para crear consultas de predicción o modelos nuevos. Para consultar algunos ejemplos sobre las llamadas a procedimientos almacenados que se pueden capturar con un seguimiento, vea [Ejemplos de consultas de modelos de agrupación en clústeres](clustering-model-query-examples.md).  
  
## <a name="see-also"></a>Consulte también  
 [Supervisión de una instancia de Analysis Services](../instances/monitor-an-analysis-services-instance.md)   
 [Use SQL Server Extended Events &#40;XEvents&#41; para supervisar Analysis Services](../instances/monitor-analysis-services-with-sql-server-extended-events.md)  
  
  
