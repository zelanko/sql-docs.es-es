---
title: Columnas de datos de eventos de comandos | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: Command Events event category
ms.assetid: 7169f1e2-c6be-4d8c-b147-25719b84bc2c
caps.latest.revision: "36"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4ca478c82617a39b311e0f627320e363a5f7127f
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="command-events-data-columns"></a>Columnas de datos de eventos de comandos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]En la tabla siguiente se enumera las columnas de datos para cada clase de eventos en el **eventos de comandos** categoría de eventos.  
  
 La categoría de eventos **Eventos de comandos** tiene las siguientes clase de eventos:  
  
-   [Clase Command Begin](#bkmk_1)  
  
-   [Clase Command End](#bkmk_2)  
  
 En las siguientes tablas se muestran las columnas de datos de cada una de estas clases de eventos.  
  
##  <a name="bkmk_1"></a> Columnas de datos de la clase Command Begin  
  
|Columna de datos|Description|  
|-----------------|-----------------|  
|ConnectionID|Contiene el Id. de conexión única asociado al evento de comando.|  
|TextData|Contiene los datos de texto asociados al evento de comando.|  
|ServerName|Contiene el nombre de la instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en la que se ha producido el evento de comando.|  
|CurrentTime|Contiene la hora actual del evento de comando.|  
|DatabaseName|Contiene el nombre de la base de datos en la que se está ejecutando el comando.|  
|EventSubclass|Contiene la clase de eventos dentro del evento de comando. Los valores admitidos son:<br /><br /> 0: Create<br /><br /> 1: Alter<br /><br /> 2: Delete<br /><br /> 3: Process<br /><br /> 4: DesignAggregations<br /><br /> 5: WBInsert<br /><br /> 6: WBUpdate<br /><br /> 7: WBDelete<br /><br /> 8: Backup<br /><br /> 9: Restore<br /><br /> 10: MergePartitions<br /><br /> 11: Subscribe<br /><br /> 12: Batch<br /><br /> 13: BeginTransaction<br /><br /> 14: CommitTransaction<br /><br /> 15: RollbackTransaction<br /><br /> 16: GetTransactionState<br /><br /> 17: Cancel<br /><br /> 18: Synchronize<br /><br /> 19: Import80MiningModels<br /><br /> 20: Attach<br /><br /> 21: Detach<br /><br /> 22: SetAuthContext<br /><br /> 23: ImageLoad<br /><br /> 24: ImageSave<br /><br /> 10000: Other|  
|NTUserName|Contiene el nombre de usuario de Windows asociado al evento de comando. El nombre de usuario está en formato canónico. Por ejemplo, engineering.microsoft.com/software/user.|  
|RequestProperties|Contiene las propiedades de solicitud de XML for Analysis (XMLA) asociadas al evento de comando.|  
|SPID|Contiene el id. de proceso de servidor (SPID) que identifica de forma única la sesión de usuario asociada al evento de comando. El SPID se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|StartTime|Contiene la hora (si está disponible) a la que se inició el evento de comando.|  
|SessionType|Contiene la entidad que ha originado la operación.|  
|NTDomainName|Contiene la cuenta de dominio de Windows asociada al evento de permiso de objeto.|  
|ClientProcessID|Contiene el Id. de proceso cliente único asociado al evento de comando.|  
  
##  <a name="bkmk_2"></a> Columnas de datos de la clase Command End  
  
|Columna de datos|Description|  
|-----------------|-----------------|  
|ConnectionID|Contiene el Id. de conexión única asociado al evento de comando.|  
|TextData|Contiene los datos de texto asociados al evento de comando.|  
|ServerName|Contiene el nombre de la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en la que se ha producido el evento de comando.|  
|CurrentTime|Contiene la hora actual del evento de comando. Para filtrar, los formatos son *AAAA*-*MM*-*DD* y *AAAA*-*MM*-*DD HH*:*MM*:*SS*.|  
|DatabaseName|Contiene el nombre de la base de datos en la que se está ejecutando el comando.|  
|Duración|Contiene el tiempo aproximado entre el inicio y el final del evento de comando.|  
|EndTime|Contiene la hora a la que finalizó el evento de comando. Para filtrar, los formatos son *AAAA*-*MM*-*DD* y *AAAA*-*MM*-*DD HH*:*MM*:*SS*.|  
|EventSubclass|Contiene la clase de eventos dentro del evento de comando. Los valores admitidos son:<br /><br /> 0: Create<br /><br /> 1: Alter<br /><br /> 2: Delete<br /><br /> 3: Process<br /><br /> 4: DesignAggregations<br /><br /> 5: WBInsert<br /><br /> 6: WBUpdate<br /><br /> 7: WBDelete<br /><br /> 8: Backup<br /><br /> 9: Restore<br /><br /> 10: MergePartitions<br /><br /> 11: Subscribe<br /><br /> 12: Batch<br /><br /> 13: BeginTransaction<br /><br /> 14: CommitTransaction<br /><br /> 15: RollbackTransaction<br /><br /> 16: GetTransactionState<br /><br /> 17: Cancel<br /><br /> 18: Synchronize<br /><br /> 19: Import80MiningModels<br /><br /> 20: Attach<br /><br /> 21: Detach<br /><br /> 22: SetAuthContext<br /><br /> 23: ImageLoad<br /><br /> 24: ImageSave<br /><br /> 10000: Other|  
|NTCanonicalUserName|Contiene el nombre de usuario de Windows asociado al evento de comando. El nombre de usuario está en formato canónico. Por ejemplo, engineering.microsoft.com/software/user.|  
|NTUserName|Contiene la cuenta de usuario de Windows asociada al evento de comando.|  
|SPID|Contiene el Id. de proceso de servidor (SPID) que define unívocamente la sesión de usuario asociada al evento de comando. El SPID se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|StartTime|Contiene la hora (si está disponible) a la que se inició el evento final de comando.|  
|CPUTime|Contiene el tiempo de CPU (en milisegundos) que el proceso utiliza entre el evento de inicio del comando y el evento final del comando.|  
|Error|Contiene el número de error de cualquier error asociado al evento de comando.|  
|Severity|Contiene el nivel de gravedad de una excepción asociada al evento de comando. Los valores son:<br /><br /> 0 = Correcto.<br /><br /> 1 = De información<br /><br /> 2 = Advertencia<br /><br /> 3 = Error|  
|Correcto|Contiene el éxito o el fracaso de un evento de comando. Los valores son:<br /><br /> 0 = Error<br /><br /> 1 = Correcto|  
|SessionType|Contiene la entidad que ha originado la operación asociada al evento final de comando.|  
|NTDomainName|Contiene la cuenta de dominio de Windows asociada al evento de comando.|  
|ClientProcessID|Contiene el Id. de proceso cliente único asociado al evento de comando.|  
  
## <a name="see-also"></a>Vea también  
 [Command Events Event Category](../../analysis-services/trace-events/command-events-event-category.md)  
  
  
