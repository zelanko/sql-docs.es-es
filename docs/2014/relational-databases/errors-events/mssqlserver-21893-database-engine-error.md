---
title: MSSQLSERVER_21893 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 21893 (Database Engine error)
ms.assetid: 1ab1195a-fe2a-4e06-b871-b177b6bea1fe
caps.latest.revision: 7
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: bf6c8b8f2ad46c1874a2b46fb74ec46c67d634c7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199361"
---
# <a name="mssqlserver21893"></a>MSSQLSERVER_21893
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|21893|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQLErrorNum21893|  
|Texto del mensaje|Los suscriptores (%s) del publicador original "%s" no aparecen como servidores remotos en el publicador redireccionado "%s". Ejecute `sp_addlinkedserver` en el publicador redirigido para agregar estos suscriptores como servidores remotos.|  
  
## <a name="explanation"></a>Explicación  
 `sp_validate_redirected_publisher` usa las tablas de metadatos de suscripción de la base de datos del publicador en el servidor remoto para identificar sus suscriptores asociados y comprueba que no hay entradas asociadas en master.dbo.sysservers para los suscriptores. Este error se devuelve si ninguno de los suscriptores identificados está presente.  
  
 Este error no se considera irrecuperable. Los agentes que encuentran este error lo registrarán como informativo pero no finalizarán, ya que un error que tenga las entradas de suscriptor adecuadas en el nuevo publicador tiene un impacto limitado en la replicación. Sin una entrada correspondiente para un suscriptor en sysservers, algunas de las actividades de administración de suscripciones pueden generar un error cuando se ejecutan a través de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. No obstante, estas mismas actividades se pueden realizar correctamente mediante la ejecución de los procedimientos almacenados de administración de forma explícita.  
  
## <a name="user-action"></a>Acción del usuario  
 Ejecute `sp_addlinkedserver` en el publicador redireccionado por cada uno de los suscriptores identificados para agregarlos como servidores remotos. A continuación, ejecute `sp_serveroption` para establecer el bit de suscriptor para el servidor.  
  
  