---
title: MSSQLSERVER_18752 | Microsoft Docs
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
- 18752 (Database Engine error)
ms.assetid: 234c58d8-7a1e-4b07-a64b-32a311527980
caps.latest.revision: 13
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: e37d24643f2c095e9b2ed15061f9b96952c5be9f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201595"
---
# <a name="mssqlserver18752"></a>MSSQLSERVER_18752
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|18752|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|REPL_INUSE|  
|Texto del mensaje|El Agente de registro del LOG y los procedimientos relacionados con el registro (sp_repldone, sp_replcmds y sp_replshowcmds) solamente pueden conectarse a la base de datos de uno en uno. Si ejecutó un procedimiento relacionado con el registro, quite la conexión mediante la cual se ejecutó el procedimiento o ejecute sp_replflush en esa conexión antes de iniciar el Agente de registro del LOG o de ejecutar otro procedimiento relacionado con el registro.|  
  
## <a name="explanation"></a>Explicación  
 Solo un Agente de registro del LOG o un procedimiento relacionado con el registro pueden conectarse a una base de datos a la vez.  
  
## <a name="user-action"></a>Acción del usuario  
 Asegúrese de que ningún otro lector del registro se esté ejecutando para la misma base de datos de publicación y que ninguna otra conexión activa se había ejecutado sp_replcmds/sp_repltrans/sp_repldone previamente sin ejecutarse sp_replflush después o desconectarse.  
  
  