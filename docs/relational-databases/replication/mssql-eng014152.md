---
title: MSSQL_ENG014152 | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014152 error
ms.assetid: 4215e2b1-cd30-441f-9671-9afc742adf6e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2014||=sqlallproducts-allversions
ms.openlocfilehash: ff2f443d5aa1811b55c9202d902b8713f6195621
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2019
ms.locfileid: "68766050"
---
# <a name="mssqleng014152"></a>MSSQL_ENG014152
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|14152|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|Replicación-%s: el agente %s está programado para reintentar. %s|  
  
## <a name="explanation"></a>Explicación  
 Se ha programado el agente de replicación especificado para volver a intentar la operación solicitada. El proceso continúa intentándolo hasta que se alcanza la cantidad máxima configurada de reintentos del paso de trabajo.  
  
 Normalmente, un reintento tiene lugar debido a uno de los siguientes motivos:  
  
-   Se supera el valor **QueryTimeout** .  
  
-   Se supera el valor **LoginTimeout** .  
  
-   El proceso de replicación fue objeto del bloqueo.  
  
## <a name="user-action"></a>Acción del usuario  
 Si el mensaje de reintento no es frecuente, no es necesaria ninguna acción por parte del usuario.  
  
 Use [sp_help_jobstep](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md) para ver la configuración actual de la cantidad máxima de reintentos del paso **Ejecutar agente** en el agente de replicación especificado. Puede utilizar el parámetro **@retry_attempts** del procedimiento almacenado [sp_update_jobstep](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md) para ajustar la cantidad de reintentos de un paso de trabajo.  
  
 Si el mensaje de reintento se repite con frecuencia, solucione el problema al que se refiere el mensaje que está causando el reintento. Busque en el historial del agente los mensajes que indiquen los motivos por los que se tuvo que programar el reintento. En algunos casos tendrá que habilitar un registro más detallado para el agente de replicación. Para obtener más información acerca de la configuración del registro para replicación, vea el artículo [312292](https://support.microsoft.com/kb/312292)de Microsoft Knowledge Base.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y eventos &#40;replicación&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
