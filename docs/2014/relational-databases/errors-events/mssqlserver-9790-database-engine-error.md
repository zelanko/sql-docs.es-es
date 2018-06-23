---
title: MSSQLSERVER_9790 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 9790 (Database Engine error)
ms.assetid: 83fd379f-5deb-4f97-8cb4-282e3d3fed94
caps.latest.revision: 13
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: abc78d3fa5ef749afc32a9a7efab6c9df9a15223
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105382"
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
  
  