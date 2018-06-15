---
title: LOCALDB_ERROR_INSTANCE_FOLDER_PATH_TOO_LONG | Documentos de Microsoft
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: performance
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: c178a308-8d99-47fc-8a49-5a480dc592f6
caps.latest.revision: 10
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 28c3c7f214ef3eff27f04c24cee8b809c063587f
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2018
ms.locfileid: "34326256"
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
  
  
