---
title: Elemento Issue (ssbdiagnose) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssbdiagnose
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- issue element
- XML output file format [ssbdiagnose], issue element
- ssbdiagnose
ms.assetid: 2246a886-686b-44ca-9771-b155cedad8be
caps.latest.revision: "17"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bb73030cc1a2788a30deea03da2892351e614d2c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="issue-element-ssbdiagnose"></a>Elemento Issue (ssbdiagnose)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Informa de un problema encontrado por el **ssbdiagnose** utilidad. El archivo de salida XML de **ssbdiagnose** tiene un elemento Issue por cada problema notificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<Issue  
    type="..."   
    code="..."   
    server="..."   
    database="..."   
    object="...">   
    ...   
</Issue>  
```  
  
## <a name="element-attributes"></a>Atributos del elemento  
  
|Attribute|Description|  
|---------------|-----------------|  
|**Tipo**|Identifica la categoría del problema sobre el que informa el elemento Issue.<br /><br /> **"Diagnóstico"** Informa de un problema de configuración encontrado al analizar una configuración de [!INCLUDE[ssSB](../../includes/sssb-md.md)] .<br /><br /> **"Problema"** Informa de un problema que ha impedido que **ssbdiagnose** complete el análisis. Corrija el problema y vuelva a ejecutar **ssbdiagnose**.<br /><br /> **"Evento"** Informa de un evento de [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] encontrado al ejecutar una comprobación de **-RUNTIME** . Solo se informa de los eventos si se especifica **-SHOWEVENTS** .|  
|**código**|Identifica el número de error del mensaje.|  
|**servidores**|Identifica la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] en la que se encontró el problema. Si el problema estaba en una instancia predeterminada, el atributo "server" solo tiene el nombre del equipo. Si el problema estaba en una instancia con nombre, el atributo "server" tiene el formato nombreDeEquipo\nombreDeInstancia.|  
|**database**|Identifica el nombre de la base de datos en la que se encontró el problema.|  
|**objeto**|Identifica el nombre del objeto en el que se encontró el problema. Si el problema era un problema de nivel de instancia o de base de datos, el atributo "object" repite el nombre de la instancia o de la base de datos.|  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Description|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|**string**, longitud ilimitada.|  
|**Value**|Devuelve el texto del mensaje de error.|  
|**Repetición**|Una vez por error notificado.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Elemento DiagnosticInformation &#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/diagnosticinformation-element-ssbdiagnose.md)|  
|**Elementos secundarios**|None|  
  
## <a name="example"></a>Ejemplo  
 Este elemento informa de un error 1102 para una base de datos que no tiene una clave maestra, en la que se encontró el error al analizar una configuración de [!INCLUDE[ssSB](../../includes/sssb-md.md)] .  
  
```  
<Issue type="Diagnosis" code="1102" server="TestComputer" database="TargetDB" object="TargetDB">The master key was not found</diagnostic>  
```  
  
## <a name="see-also"></a>Vea también  
 [Utilidad ssbdiagnose &#40;Service Broker&#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
  
