---
title: MSSQL_ENG021331 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG021331 error
ms.assetid: 9acd75d9-fda1-44cd-ba17-20295ad53ea0
caps.latest.revision: 15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4bab3ee3277554b3e3846e95c17f44e1cc937a17
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37298085"
---
# <a name="mssqleng021331"></a>MSSQL_ENG021331
    
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
  
## <a name="see-also"></a>Vea también  
 [Specify the Default Snapshot Location &#40;SQL Server Management Studio&#41;](specify-the-default-snapshot-location-sql-server-management-studio.md)  (Especificar la ubicación predeterminada de instantáneas [SQL Server Management Studio])  
 [Referencia de errores y eventos &#40;replicación&#41;](errors-and-events-reference-replication.md)   
 [Initialize a Transactional Subscription Without a Snapshot](initialize-a-transactional-subscription-without-a-snapshot.md) (Inicializar una suscripción transaccional sin una instantánea)  
  
  
