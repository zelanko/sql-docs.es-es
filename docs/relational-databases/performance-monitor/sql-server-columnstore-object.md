---
title: Columnstore (objeto de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 04/12/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: ae663a49-012f-4ffe-a332-f03157843052
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 334a8388b7abc217123071fdc37c9e1091f6a3fc
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "67987136"
---
# <a name="sql-server-columnstore-object"></a>Objeto Columnstore de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  El objeto **SQLServer:Columnstore** proporciona contadores para supervisar la ejecución de índices de almacén de columnas en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 En la siguiente tabla se describen los contadores de **Columnstore** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Contadores de Columnstore|Descripción|  
|--------------------------|-----------------|  
|**Grupos de filas delta cerrados**|Número de grupos de filas delta cerrados.|  
|**Grupos de filas delta comprimidos**|Número de grupos de filas delta comprimidos.|  
|**Grupos de filas delta creados**|Número de grupos de filas delta creados.|  
|**Frecuencia de aciertos de caché de segmentos**|Porcentaje de segmentos de columna que se han encontrado en el grupo del almacén de columnas sin tener que incurrir en una lectura de disco.|  
|**Base de frecuencia de aciertos de caché de segmento**|Solo para uso interno.|
|**Lecturas de segmento por segundo**|Número de lecturas de segmento físico emitidas.|  
|**Total de búferes de eliminación migrados**|Número de veces que el motor de tupla ha limpiado el búfer de eliminación.|  
|**Total de evaluaciones de directiva de combinación**|Número de veces que se ha evaluado la directiva de combinación para el almacén de columnas.|  
|**Total de grupos de filas comprimidos**|Número total de grupos de filas comprimidos.|  
|**Grupos de filas totales aptas para Merge**|Número de grupos de filas de origen aptas para una operación MERGE desde el inicio de SQL Server.|  
|**Total de grupos de filas comprimidos de combinación**|Número de grupos de filas de destino comprimidos creados con MERGE desde el inicio de SQL Server.|  
|**Total de grupos de filas de origen combinados**|Número de grupos de filas de origen combinados desde el inicio de SQL Server.|  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
