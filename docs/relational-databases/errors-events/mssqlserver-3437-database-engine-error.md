---
title: MSSQLSERVER_3437 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 3437 (Database Engine error)
ms.assetid: b38216e2-b650-43bd-97af-061d54f60031
caps.latest.revision: 17
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 09606529603f3e7c0747674724d8457872465eff
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver3437"></a>MSSQLSERVER_3437
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|3437|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|NODTC|  
|Texto del mensaje|Error al recuperar la base de datos '%.*ls'. No se puede conectar con Microsoft DTC (Coordinador de transacciones distribuidas) para comprobar el estado de finalización de la transacción %S_XID. Corrija MS DTC y vuelva a ejecutar la recuperación.|  
  
## <a name="explanation"></a>Explicación  
Una o más transacciones distribuidas que estaban usando el Coordinador de transacciones distribuidas de [!INCLUDE[msCoName](../../includes/msconame-md.md)] (MS DTC) estaban incompletas cuando se cerró la base de datos. Se originó un error al recuperar la base de datos debido a que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se puede conectar a MS DTC para completar o revertir las transacciones.  
  
## <a name="user-action"></a>Acción del usuario  
Para recuperar esta base de datos, primero debe resolver el problema con MS DTC. Para estudiar el problema con MS DTC, examine los registros de eventos de Windows. Si no puede resolver el problema con MS DTC y recuperar la base de datos, restaure una copia de seguridad de la base de datos.  
  
