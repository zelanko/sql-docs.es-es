---
title: MSSQL_ENG020596 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG020596 error
ms.assetid: fa33627c-2e99-4be3-9424-52ab83446e07
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8b1c61f3683442e0d474ff36a65c89446dbd7bd1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85010228"
---
# <a name="mssql_eng020596"></a>MSSQL_ENG020596
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|20596|  
|Origen de eventos|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|Solo '%1!' o los miembros de db_owner pueden quitar el agente anónimo.|  
  
## <a name="explanation"></a>Explicación  
 No tiene suficientes permisos para quitar el agente de la suscripción anónima. El inicio de sesión usado al llamar a [sp_dropanonymousagent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropanonymousagent-transact-sql) debe ser un miembro del rol fijo de servidor **sysadmin** del distribuidor o del rol fijo de base de datos **db_owner** de la base de datos de distribución, o bien el usuario debe ser el que inició la primera ejecución del agente.  
  
## <a name="user-action"></a>Acción del usuario  
 Inicie sesión con las credenciales correctas y ejecute **sp_dropanonymousagent**.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y eventos &#40;replicación&#41;](errors-and-events-reference-replication.md)  
  
  
