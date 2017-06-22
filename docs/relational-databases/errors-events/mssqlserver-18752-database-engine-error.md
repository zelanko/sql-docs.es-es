---
title: MSSQLSERVER_18752 | Microsoft Docs
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
- 18752 (Database Engine error)
ms.assetid: 234c58d8-7a1e-4b07-a64b-32a311527980
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ce8ebaa18b057d5d49240665eff67afcc7720418
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

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
  

