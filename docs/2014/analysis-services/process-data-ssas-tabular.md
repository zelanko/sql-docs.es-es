---
title: Procesar datos (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: d88f2dc9-2933-4be5-9bf3-48ffbc2d0a1a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c3f47ddcfab5df43104d3998822fdaf8bd504946
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48048435"
---
# <a name="process-data-ssas-tabular"></a>Procesar datos (SSAS tabular)
  Cuando se importan datos en un modelo tabular en modo de almacenamiento en caché, se captura una instantánea de esos datos en el momento de la importación. En algunos casos, esos datos nunca cambian y no es necesario actualizarlos en el modelo. Sin embargo, es más probable que los datos que se importan cambien con regularidad, y para que el modelo refleje los datos más recientes de los orígenes de datos, es necesario procesar (actualizar) los datos y recalcular los datos calculados. Para actualizar los datos del modelo, deberá realizar una acción de procesamiento en todas las tablas o en una tabla individual, mediante una partición o mediante una conexión de origen de datos.  
  
 Al crear el proyecto de modelos, las acciones de procesamiento se deben iniciar manualmente en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Una vez implementado el modelo, las operaciones de procesamiento se pueden realizar utilizando [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] o programar mediante un script. Todas las tareas aquí descritas pertenecen a acciones de procesamiento que puede realizar durante la creación de modelos en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Para obtener más información sobre las acciones de procesamiento para un modelo implementado, vea [Process Database, Table, or Partition](tabular-models/process-database-table-or-partition-analysis-services.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Procesar manualmente los datos &#40;Tabular de SSAS&#41;](manually-process-data-ssas-tabular.md)|Describe cómo procesar manualmente los datos del área de trabajo del modelo.|  
|[Solución de problemas de procesamiento de datos &#40;Tabular de SSAS&#41;](troubleshoot-process-data-ssas-tabular.md)|Describe cómo solucionar problemas de operaciones de proceso.|  
  
  
