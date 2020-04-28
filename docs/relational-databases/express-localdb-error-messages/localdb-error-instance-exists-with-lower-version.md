---
title: LOCALDB_ERROR_INSTANCE_EXISTS_WITH_LOWER_VERSION | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: reference
ms.assetid: a7c5ce08-8841-49a3-b252-116807ba469a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5f86efc789bd978606dfa5528191f24dcdc70ff6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67995843"
---
# <a name="localdb_error_instance_exists_with_lower_version"></a>LOCALDB_ERROR_INSTANCE_EXISTS_WITH_LOWER_VERSION
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|258|  
|Origen de eventos|SQL Server Local Database Runtime 12.0|  
|Componente|API de Local Database Runtime|  
|Texto del mensaje|No se puede crear la instancia de Local Database con la versión especificada. Ya existe una instancia con el mismo nombre, pero tiene una versión anterior a la versión especificada.|  
  
## <a name="explanation"></a>Explicación  
 La instancia especificada ya existe pero la versión es anterior a la solicitada.  
  
## <a name="user-action"></a>Acción del usuario  
 Elimine la instancia existente e intente de nuevo la operación.  
  
  
