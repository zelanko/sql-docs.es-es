---
title: Automatizar tareas administrativas de Analysis Services con SSIS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Execute DDL Task [Analysis Services]
- Analysis Services Processing task
ms.assetid: e960a9a2-80b4-45da-9369-bc560ecdccac
caps.latest.revision: 29
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 35ba767c2c6d0b230a3515a8e5df48d6f126284a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37251147"
---
# <a name="automate-analysis-services-administrative-tasks-with-ssis"></a>Automatizar tareas administrativas de Analysis Services con SSIS
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] permite automatizar la ejecución de scripts DDL, tareas de procesamiento de cubos y modelos de minería de datos, y tareas de consulta de minería de datos. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] puede considerarse como una colección de tareas de flujo de control y de mantenimiento, que pueden vincularse para formar trabajos de procesamiento de datos secuenciales y paralelos.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se ha diseñado para realizar operaciones de limpieza de datos durante las tareas de procesamiento y para reunir datos procedentes de diferentes orígenes de datos. Cuando se trabaja con cubos y modelos de minería de datos, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] puede transformar datos no numéricos en datos numéricos y puede garantizar que esos valores de datos se encuentran dentro de los límites esperados, creando así datos limpios desde los cuales llenar dimensiones y tablas de hechos.  
  
## <a name="integration-services-tasks"></a>Tareas de Integration Services  
 Existen dos elementos principales en cualquier tarea o trabajo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] : elementos de flujo de control y elementos de flujo de datos. Los elementos de flujo de control definen el orden lógico de la progresión del trabajo aplicando restricciones de precedencia. Los elementos de flujo de datos se refieren a la conectividad entre la salida de un componente y la entrada del componente siguiente y a cualquier transformación de datos que puede llevarse a cabo en los datos entre ambas acciones. En cuanto a la decisión sobre el destino de los datos, las restricciones de precedencia contienen lógica que especifica qué componente recibe la salida. Las tareas de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] más relevantes para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] incluyen las tareas Ejecutar DDL, Procesamiento de Analysis Services y Consulta de minería de datos. Para cada una de estas tareas, se puede utilizar la tarea Enviar correo para enviar al administrador un mensaje de correo electrónico que contenga los resultados de la tarea.  
  
## <a name="the-execute-ddl-task"></a>Tarea Ejecutar DDL  
 La tarea Ejecutar DDL de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] permite enviar directamente scripts DDL al servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y ejecutarlos de forma automática. Esto permite que el administrador de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] realice operaciones de copia de seguridad, de restauración o de sincronización desde un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Un paquete se compone de los elementos de flujo de control y de flujo de datos descritos anteriormente. Todos se deben **run regularly**, al igual que otras instrucciones DDL que pueden agregarse a las tareas. Debido a que las tareas aquí tratadas se ejecutan frecuentemente en horario nocturno, resulta especialmente útil disponer de paquetes que puede ejecutarse con facilidad desde cualquier aplicación de programación. Puede programar que un paquete se ejecute en cualquier momento usando el Agente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para obtener más información sobre cómo implementar esta tarea, vea [Tarea Ejecutar DDL de Analysis Services](../../integration-services/control-flow/analysis-services-execute-ddl-task.md).  
  
## <a name="analysis-services-processing-task"></a>Procesamiento de Analysis Services, tarea  
 La tarea Procesamiento de Analysis Services de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] permite llenar automáticamente los cubos con nueva información cuando se realizan actualizaciones periódicas de la base de datos relacional de origen. Puede realizar el procesamiento en el nivel de dimensión, de cubo o de partición mediante la tarea Procesamiento de Analysis Services. El propio procesamiento puede ser de tipo `incremental` o `full`; esta opción se selecciona basándose en los requisitos del trabajo. El procesamiento incremental agrega nuevos datos y lleva a cabo suficiente trabajo de cálculo para mantener actualizado el destino, en tanto que el procesamiento completo realiza una nueva carga y un nuevo cálculo completos de los datos existentes. El procesamiento completo requiere más tiempo, pero es más absoluto. Para obtener más información acerca de cómo implementar esta tarea, vea [Analysis Services Processing Task](../../integration-services/control-flow/analysis-services-processing-task.md).  
  
## <a name="data-mining-query-task"></a>Data Mining Query Task  
 La tarea Consulta de minería de datos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] permite extraer y almacenar información de los modelos de minería de datos. Por lo general, la información se almacena en una base de datos relacional y puede utilizarse, por ejemplo, para aislar una lista de clientes potenciales para una campaña de correo directo. La minería de datos puede identificar el valor de un cliente y la probabilidad de que ese cliente responda a una determinada acción de marketing. Puede utilizar la tarea Consulta de minería de datos para extraer y modificar datos en un formato de preferencia. Para obtener más información acerca de cómo implementar esta tarea, vea [Data Mining Query Task](../../integration-services/control-flow/data-mining-query-task.md).  
  
## <a name="see-also"></a>Vea también  
 [Destino de procesamiento de particiones](../../integration-services/data-flow/partition-processing-destination.md)   
 [Destino de procesamiento de dimensiones](../../integration-services/data-flow/dimension-processing-destination.md)   
 [Transformación consulta de minería de datos](../../integration-services/data-flow/transformations/data-mining-query-transformation.md)   
 [Procesamiento de objetos de modelo multidimensional](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Secuencia de comandos de las tareas administrativas en Analysis Services](../script-administrative-tasks-in-analysis-services.md)  
  
  
