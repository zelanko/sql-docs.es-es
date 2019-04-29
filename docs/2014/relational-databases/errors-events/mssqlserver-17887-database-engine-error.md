---
title: MSSQLSERVER_17887 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 17887 (Database Engine error)
ms.assetid: ad0806e6-3296-4c32-b103-fccf0f8a8d3d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3de0d505f99fd1f8f7da968bde13eb56fe50efc1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62915212"
---
# <a name="mssqlserver17887"></a>MSSQLSERVER_17887
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|17887|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SRV_IO_COMP_LISTENER_NONYIELDING|  
|Texto del mensaje|Parece que la escucha de finalización de E/S (0x%lx) Trabajo 0x%p no rinde en el nodo %ld. Uso de CPU (aprox.): kernel %I64d ms, usuario %I64d ms, Intervalo: %I64d.|  
  
## <a name="explanation"></a>Explicación  
Indica que hay un posible problema con la escucha del puerto de finalización de E/S en el nodo especificado al ejecutar la rutina de finalización de E/S para un evento de lectura/escritura de red. Este error desaparecerá cuando la escucha del puerto de finalización de E/S vuelva de ejecutar la rutina de finalización de E/S.  
  
## <a name="user-action"></a>Acción del usuario  
Póngase en contacto con los servicios de soporte al cliente de Microsoft (CSS).  
  
