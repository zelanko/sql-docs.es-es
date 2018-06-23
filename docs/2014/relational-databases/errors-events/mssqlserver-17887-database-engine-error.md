---
title: MSSQLSERVER_17887 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 17887 (Database Engine error)
ms.assetid: ad0806e6-3296-4c32-b103-fccf0f8a8d3d
caps.latest.revision: 17
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 6278d6c4e46f644bfdf0f062f7a94f2bf878f316
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107659"
---
# <a name="mssqlserver17887"></a>MSSQLSERVER_17887
    
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
  
  