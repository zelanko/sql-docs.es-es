---
title: MSSQLSERVER_9790 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 9790 (Database Engine error)
ms.assetid: 83fd379f-5deb-4f97-8cb4-282e3d3fed94
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f7a07e157da848a3201d0a50d6e270988ddf9943
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver9790"></a>MSSQLSERVER_9790
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|9790|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SB3_XMIT_ERROR_ENTRANCE_BROKER_SINGLE_USER|  
|Texto del mensaje|No se puede enrutar el mensaje entrante. La base de datos del sistema MSDB que contiene la información de enrutamiento está en modo SINGLE USER.|  
  
## <a name="explanation"></a>Explicación  
Se produjo un error al intentar clasificar un mensaje recibido fuera de la conexión porque la base de datos MSDB estaba en modo SINGLE USER.  
  
## <a name="user-action"></a>Acción del usuario  
Cambie MSDB para que esté en modo MULTI USER con el comando ALTER DATABASE.  
  

