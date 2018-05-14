---
title: MSSQLSERVER_1462 | Microsoft Docs
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
- 1462 (Database Engine error)
ms.assetid: 680e9c1c-a9d6-4765-b601-956d0a83324c
caps.latest.revision: 12
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 15056343576f10b09dad46e7cbe543847fd5bafa
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver1462"></a>MSSQLSERVER_1462
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|1462|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBM_DISABLED_DUE_TO_FAILED_REDO|  
|Texto del mensaje|La creación de reflejo de la base de datos está deshabilitada debido a una operación de puesta al día con errores. No se puede reanudar.|  
  
## <a name="explanation"></a>Explicación  
La creación de reflejo de la base de datos no puede poner al día una entrada de registro en el reflejo.  
  
### <a name="possible-causes"></a>Posibles causas  
La causa más probable es que se haya completado una operación de agregar archivos en la base de datos principal pero que haya generado un error en la base de datos reflejada al ser diferentes los nombres de archivo o estructuras de directorio en el servidor principal y reflejado.  
  
## <a name="user-action"></a>Acción del usuario  
Busque la causa de este error en el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Intente resolver la causa y reanude la creación de reflejo de la base de datos.  
  
## <a name="see-also"></a>Ver también  
[Solucionar problemas de configuración de creación de reflejo de la base de datos &#40;SQL Server&#41;](~/database-engine/database-mirroring/troubleshoot-database-mirroring-configuration-sql-server.md)  
  
