---
title: MSSQLSERVER_21871 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 21871 (Database Engine error)
ms.assetid: d3215378-9282-444f-a18b-00b96fd0133d
caps.latest.revision: 6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e0ae46f9de027e518e8819e08439771b1b3e52a1
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2018
---
# <a name="mssqlserver21871"></a>MSSQLSERVER_21871
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|21871|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQLErrorNum21871|  
|Texto del mensaje|El publicador %s de la base de datos %s no ha sido redirigido.|  
  
## <a name="explanation"></a>Explicación  
**sp_validate_replica_hosts_as_publishers** busca una entrada para el publicador identificado y la base de datos del publicador en la tabla MSredirected_publishers de la base de datos de distribución.  **sp_validate_replica_hosts_as_publishers** devuelve el error 21871 si no se encuentra ninguna entrada.  
  
## <a name="user-action"></a>Acción del usuario  
**sp_validate_replica_hosts_as_publishers** solo es pertinente para los publicadores redirigidos. Si la base de datos del publicador es miembro de un grupo de disponibilidad, use el procedimiento almacenado **sp_redirect_publisher** para asociar el publicador y la base de datos del publicador con el nombre de escucha de grupo de disponibilidad del grupo de disponibilidad.  
  
