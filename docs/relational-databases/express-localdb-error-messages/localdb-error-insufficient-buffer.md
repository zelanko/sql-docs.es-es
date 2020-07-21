---
title: LOCALDB_ERROR_INSUFFICIENT_BUFFER | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: ff67bda8-7e5c-4b06-8d7b-9985b6059a98
author: stevestein
ms.author: sstein
ms.openlocfilehash: 8b21d9137483b7d7b76c6e91f0fd44363bf58f7c
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85641795"
---
# <a name="localdb_error_insufficient_buffer"></a>LOCALDB_ERROR_INSUFFICIENT_BUFFER
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|276|  
|Origen de eventos|SQL Server Local Database Runtime 12.0|  
|Componente|API de Local Database Runtime|  
|Texto del mensaje|El búfer pasado el método de API de la instancia de Local Database no tiene un tamaño suficiente.|  
  
## <a name="explanation"></a>Explicación  
 El búfer de entrada es demasiado corto y no se ha solicitado truncamiento.  
  
## <a name="user-action"></a>Acción del usuario  
 Proporcione un búfer del tamaño especificado.  
  
  
