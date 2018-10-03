---
title: MSSQL_ENG021798 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021798 error
ms.assetid: 596f5092-75ab-4a19-8582-588687c7b089
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0cadc615110b6d0d3999a1408d320a2476a0394d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48097705"
---
# <a name="mssqleng021798"></a>MSSQL_ENG021798
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|21798|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|Debe agregar el trabajo de agente '%s' a través de '%s' antes de continuar. Vea la documentación de '%s'.|  
  
## <a name="explanation"></a>Explicación  
 Para crear una publicación hay que ser miembro del rol fijo de servidor **sysadmin** en el publicador o miembro del rol fijo de base de datos **db_owner** de la base de datos de la publicación. Si es miembro del rol **db_owner** , este error se produce cuando:  
  
-   Se ejecutan scripts desde [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)]. El modelo de seguridad de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]ha cambiado, por lo que dichos scripts deben actualizarse.  
  
-   El procedimiento almacenado **sp_addpublication** se ejecuta antes de ejecutar [sp_addlogreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql). Esto es aplicable a todas las publicaciones transaccionales.  
  
-   El procedimiento almacenado **sp_addpublication** se ejecuta antes de ejecutar [sp_addqreader_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addqreader-agent-transact-sql). Esto se aplica a las publicaciones transaccionales habilitadas para suscripciones de actualización en cola (un valor de TRUE para el parámetro **@allow_queued_tran** de **sp_addpublication**).  
  
 Cada uno de los procedimientos almacenados **sp_addlogreader_agent** y **sp_addqreader_agent** crea un trabajo de agente y permite especificar la cuenta de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows con la que se ejecuta el agente. Para los usuarios del rol **sysadmin** , los trabajos de agente se crean de forma implícita si **sp_addlogreader_agent** y **sp_addqreader_agent** no se ejecutan; los agentes se ejecutan en el contexto de la cuenta de servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el distribuidor. Aunque **sp_addlogreader_agent** y **sp_addqreader_agent** no son necesarios para los usuarios del rol **sysadmin** , por motivos de seguridad se recomienda especificar una cuenta independiente para los agentes. Para más información, consulte [Modelo de seguridad del agente de replicación](security/replication-agent-security-model.md).  
  
## <a name="user-action"></a>Acción del usuario  
 Asegúrese de ejecutar los procedimientos en el orden correcto. Para obtener más información, consulte [crear una publicación](publish/create-a-publication.md), actualice dichos scripts para incluir los procedimientos almacenados y los parámetros requeridos por [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores. Para obtener más información, vea [Actualizar scripts de replicación &#40;programación de la replicación con Transact-SQL&#41;](administration/upgrade-replication-scripts-replication-transact-sql-programming.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y eventos &#40;replicación&#41;](errors-and-events-reference-replication.md)  
  
  
