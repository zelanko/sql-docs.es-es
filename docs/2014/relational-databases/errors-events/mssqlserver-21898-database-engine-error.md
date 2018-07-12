---
title: MSSQLSERVER_21898 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 21898 (Database Engine error)
ms.assetid: 02405b21-3d4e-4c2d-b4b3-d7b1ec05edb4
caps.latest.revision: 7
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 551b199b6c4c97b58eca822e1372d3b51af31585
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37423464"
---
# <a name="mssqlserver21898"></a>MSSQLSERVER_21898
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|21898|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQLErrorNum21898|  
|Texto del mensaje|El publicador '%s' usa la base de datos de distribución '%s' y no '%s', que se requiere para hospedar la base de datos de publicación '%s'. Ejecute `sp_changedistpublisher` en el distribuidor para cambiar la base de datos de distribución que usa el publicador por '%s'.|  
  
## <a name="explanation"></a>Explicación  
 `sp_validate_redirected_publisher` consulta a msdb.dbo.MSdistpublishers en el distribuidor local para comprobar que la base de datos de distribución utilizada por el nuevo publicador es el mismo que la base de datos de distribución utilizada por el publicador original. Este error se devuelve cuando estas bases de datos son distintas, con lo que el editor no es un host adecuado para la base de datos del publicador.  
  
## <a name="user-action"></a>Acción del usuario  
 Ejecute el procedimiento almacenado `sp_changedistpublisher` para cambiar la base de datos de distribución para el nuevo publicador por la usada por el publicador original.  
  
> [!NOTE]  
>  La ejecución de `sp_changedistpublisher` corregirá el problema si se ha especificado una base de datos de distribución errónea cuando `sp_adddistpublisher` se ejecutó en el distribuidor para el publicador. No obstante, si el publicador remoto tiene publicaciones existentes de otra base de datos de publicación que haga uso de la base de datos de distribución identificada, este cambio no resulta adecuado. La replicación con la base de datos de distribución con nombre se debe quitar sistemáticamente y, a continuación, se debe volver a establecer con la base de datos de distribución del publicador original para que el publicador nuevo funcione como un host adecuado.  
  
  
