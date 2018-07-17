---
title: MSSQL_ENG021331 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: replication
ms.reviewer: ''
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021331 error
ms.assetid: 9acd75d9-fda1-44cd-ba17-20295ad53ea0
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 74a16f87c98420b04ee086f56aae80b120285b94
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37353727"
---
# <a name="mssqleng021331"></a>MSSQL_ENG021331
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|21331|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|No se pudo copiar el archivo de script de usuario en el distribuidor.(%ls)|  
  
## <a name="explanation"></a>Explicación  
 Este error puede ocurrir cuando se inicializa manualmente una suscripción y no es posible guardar en el directorio especificado los scripts generados por la replicación o especificados en un comando de replicación. Este error puede deberse a un problema de permisos: cuando se inicializa una suscripción sin utilizar una instantánea, la cuenta con la que se ejecuta el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el publicador debe tener permisos de escritura para la carpeta de la instantánea en el distribuidor.  
  
## <a name="user-action"></a>Acción del usuario  
 Compruebe que se ha especificado la ruta de acceso correcta para la carpeta de instantáneas y que la cuenta con la que se ejecuta el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el publicador dispone de permisos suficientes.  
  
## <a name="see-also"></a>Ver también  
 [Specify the Default Snapshot Location &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/specify-the-default-snapshot-location-sql-server-management-studio.md)  (Especificar la ubicación predeterminada de instantáneas [SQL Server Management Studio])  
 [Referencia de errores y eventos &#40;replicación&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Initialize a Transactional Subscription Without a Snapshot](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md) (Inicializar una suscripción transaccional sin una instantánea)  
  
  
