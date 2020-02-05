---
title: MSSQLSERVER_21871 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 21871 (Database Engine error)
ms.assetid: d3215378-9282-444f-a18b-00b96fd0133d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: fa8d7f1a92891cc2dcdabc431dcf97a1392201c1
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68056702"
---
# <a name="mssqlserver_21871"></a>MSSQLSERVER_21871
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|21871|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQLErrorNum21871|  
|Texto del mensaje|El publicador %s de la base de datos %s no ha sido redirigido.|  
  
## <a name="explanation"></a>Explicación  
**sp_validate_replica_hosts_as_publishers** busca una entrada para el publicador identificado y la base de datos del publicador en la tabla MSredirected_publishers de la base de datos de distribución.  **sp_validate_replica_hosts_as_publishers** devuelve el error 21871 si no se encuentra ninguna entrada.  
  
## <a name="user-action"></a>Acción del usuario  
**sp_validate_replica_hosts_as_publishers** solo es pertinente para los publicadores redirigidos. Si la base de datos del publicador es miembro de un grupo de disponibilidad, use el procedimiento almacenado **sp_redirect_publisher** para asociar el publicador y la base de datos del publicador con el nombre de escucha de grupo de disponibilidad del grupo de disponibilidad.  
  
