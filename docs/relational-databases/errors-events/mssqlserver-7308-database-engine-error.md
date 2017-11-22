---
title: MSSQLSERVER_7308 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 7308 (Database Engine error)
- single-threaded apartment mode
ms.assetid: cca9eab9-afb9-463d-abfd-0802257e2c99
caps.latest.revision: "7"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5cf8216f916b6dbfe501f85fe18a5c6990a03762
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver7308"></a>MSSQLSERVER_7308
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|7308|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|RMT_STA_DISABLED|  
|Texto del mensaje|El proveedor OLE DB '%ls' no puede usarse para consultas distribuidas porque está configurado para ejecutarse en el modo de subprocesamiento controlado simple.|  
  
## <a name="explanation"></a>Explicación  
Ha utilizado un proveedor OLE DB que está configurado para ejecutarse en modo de subprocesamiento controlado simple (STA). Los proveedores OLE DB que se ejecutan en modo de subprocesamiento controlado simple (STA) no se pueden utilizar para consultas distribuidas.  
  
## <a name="user-action"></a>Acción del usuario  
Para resolver este error, configure el proveedor para ejecutarse en modo de contenedor multiproceso (MTA). Si el proveedor no admite MTA y no puede realizar una actualización a una versión que admita MTA, considere la posibilidad de configurarlo para ejecutarse fuera de proceso. El fabricante del proveedor debe indicarle si éste admite MTA o si se ha de ejecutar fuera de proceso.  
  
