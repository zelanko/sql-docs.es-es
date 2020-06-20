---
title: MSSQLSERVER_21871 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 21871 (Database Engine error)
ms.assetid: d3215378-9282-444f-a18b-00b96fd0133d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: f26211da21829a0a898dfb36ff9fefd453c7ad44
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85034651"
---
# <a name="mssqlserver_21871"></a>MSSQLSERVER_21871
    
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
 `sp_validate_replica_hosts_as_publishers` busca en la tabla MSredirected_publishers en la base de datos de distribución una entrada para el publicador identificado y la base de datos del publicador.  `sp_validate_replica_hosts_as_publishers` devuelve el error 21871 cuando no se encuentra ninguna entrada.  
  
## <a name="user-action"></a>Acción del usuario  
 `sp_validate_replica_hosts_as_publishers` solo es relevante para los publicadores redirigidos. Si la base de datos del publicador es miembro de un grupo de disponibilidad, use el procedimiento almacenado `sp_redirect_publisher` para asociar el publicador y la base de datos del publicador con el nombre de escucha de grupo de disponibilidad del grupo de disponibilidad.  
  
  
