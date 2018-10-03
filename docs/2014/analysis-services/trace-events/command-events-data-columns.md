---
title: Columnas de datos de eventos de comandos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Command Events event category
ms.assetid: 7169f1e2-c6be-4d8c-b147-25719b84bc2c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ce551de71785fb947283674771b23399bfc7417f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48219915"
---
# <a name="command-events-data-columns"></a>Columnas de datos de eventos de comandos
  En la tabla siguiente se enumeran las columnas de datos para cada clase de eventos de la categoría de eventos **Eventos de comandos** .  
  
 La categoría de eventos **Eventos de comandos** tiene las siguientes clase de eventos:  
  
-   [Clase Command Begin](#bkmk_1)  
  
-   [Clase Command End](#bkmk_2)  
  
 En las siguientes tablas se muestran las columnas de datos de cada una de estas clases de eventos.  
  
##  <a name="bkmk_1"></a> Columnas de datos de la clase Command Begin  
  
|Columna de datos|Descripción|  
|-----------------|-----------------|  
|ConnectionID|Contiene el Id. de conexión única asociado al evento de comando.|  
|TextData|Contiene los datos de texto asociados al evento de comando.|  
|ServerName|Contiene el nombre de la instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en la que se ha producido el evento de comando.|  
|CurrentTime|Contiene la hora actual del evento de comando.|  
|DatabaseName|Contiene el nombre de la base de datos en la que se está ejecutando el comando.|  
|EventSubclass|Contiene la clase de eventos dentro del evento de comando. Los valores son:<br /><br /> 0: Create<br />1: Alter<br />2: Delete<br />3: Process<br />4: DesignAggregations<br />5: WBInsert<br />6: WBUpdate<br />7: WBDelete<br />8: Backup<br />9: Restore<br />10: MergePartitions<br />11: Subscribe<br />12: Batch<br />13: BeginTransaction<br />14: CommitTransaction<br />15: RollbackTransaction<br />16: GetTransactionState<br />17: Cancel<br />18: Synchronize<br />19: Import80MiningModels<br />20: Attach<br />21: Detach<br />22: SetAuthContext<br />23: ImageLoad<br />24: ImageSave<br />10000: Other|  
|NTUserName|Contiene el nombre de usuario de Windows asociado al evento de comando. El nombre de usuario está en formato canónico. Por ejemplo, engineering.microsoft.com/software/user.|  
|RequestProperties|Contiene las propiedades de solicitud de XML for Analysis (XMLA) asociadas al evento de comando.|  
|SPID|Contiene el id. de proceso de servidor (SPID) que identifica de forma única la sesión de usuario asociada al evento de comando. El SPID se corresponde directamente con el GUID de sesión utilizado por XMLA.|  
|StartTime|Contiene la hora (si está disponible) a la que se inició el evento de comando.|  
|SessionType|Contiene la entidad que ha originado la operación.|  
|NTDomainName|Contiene la cuenta de dominio de Windows asociada al evento de permiso de objeto.|  
|ClientProcessID|Contiene el Id. de proceso cliente único asociado al evento de comando.|  
  
##  <a name="bkmk_2"></a> Columnas de datos de la clase Command End  
  
|Columna de datos|Descripción|  
|-----------------|-----------------|  
|ConnectionID|Contiene el Id. de conexión única asociado al evento de comando.|  
|TextData|Contiene los datos de texto asociados al evento de comando.|  
|ServerName|Contiene el nombre de la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en la que se ha producido el evento de comando.|  
|CurrentTime|Contiene la hora actual del evento de comando. Para filtrar, los formatos son *AAAA*-*MM*-*DD* y *AAAA*-*MM*-*DD HH*:*MM*:*SS*.|  
|DatabaseName|Contiene el nombre de la base de datos en la que se está ejecutando el comando.|  
|Duration|Contiene el tiempo aproximado entre el inicio y el final del evento de comando.|  
|EndTime|Contiene la hora a la que finalizó el evento de comando. Para filtrar, los formatos son *AAAA*-*MM*-*DD* y *AAAA*-*MM*-*DD HH*:*MM*:*SS*.|  
|EventSubclass|Contiene la clase de eventos dentro del evento de comando. Los valores son:<br /><br /> 0: Create<br />1: Alter<br />2: Delete<br />3: Process<br />4: DesignAggregations<br />5: WBInsert<br />6: WBUpdate<br />7: WBDelete<br />8: Backup<br />9: Restore<br />10: MergePartitions<br />11: Subscribe<br />12: Batch<br />13: BeginTransaction<br />14: CommitTransaction<br />15: RollbackTransaction<br />16: GetTransactionState<br />17: Cancel<br />18: Synchronize<br />19: Import80MiningModels<br />20: Attach<br />21: Detach<br />22: SetAuthContext<br />23: ImageLoad<br />24: ImageSave<br />10000: Other|  
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
 [Categoría de eventos Eventos de comandos](command-events-event-category.md)  
  
  
