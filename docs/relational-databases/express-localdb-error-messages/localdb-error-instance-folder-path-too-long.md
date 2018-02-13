---
title: LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: localdb
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: c178a308-8d99-47fc-8a49-5a480dc592f6
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 53a553f454b89133b083c03fa492effd8ec12e97
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2018
---
# <a name="localdberrorinstancefolderpathtoolong"></a>LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|260|  
|Origen del evento|SQL Server Local Database Runtime 12.0|  
|Componente|API de Local Database Runtime|  
|Texto del mensaje|La longitud de la ruta de acceso completa de la carpeta de la instancia de Local Database es mayor que MAX_PATH. La instancia debe almacenarse en la carpeta: %%LOCALAPPDATA%%\Microsoft\Microsoft SQL Server Local DB\Instances\\< nombre de instancia\>.|  
  
## <a name="explanation"></a>Explicación  
 La ruta de acceso donde la instancia debe almacenarse es mayor que MAX_PATH.  
  
## <a name="user-action"></a>Acción del usuario  
 Cree una nueva ruta de acceso que sea menor que MAX_PATH.  
  
  
