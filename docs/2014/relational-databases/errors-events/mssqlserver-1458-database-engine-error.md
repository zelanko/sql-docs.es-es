---
title: MSSQLSERVER_1458 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 1458 (Database Engine error)
ms.assetid: adc78c59-a6f2-432b-9a07-fdd1dc2b9026
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 6a62738b8d4205e269e51d45c98cfd114c3451fe
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84969585"
---
# <a name="mssqlserver_1458"></a>MSSQLSERVER_1458
    
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|1458|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBM_FAILREDO_ON_PRIMARY|  
|Texto del mensaje|La copia principal de la base de datos '%.*ls' encontró el error %d, el estado %d y la gravedad %d. Se suspendió la creación de reflejos de la base de datos. Intente resolver la condición de error y reanude la creación de reflejo.|  
  
## <a name="explanation"></a>Explicación  
 Este mensaje indica que la base de datos principal encontró un error que ocasionó la suspensión de la creación de reflejo de la base de datos.  
  
## <a name="user-action"></a>Acción del usuario  
 En la mayoría de los casos, este error se corrige automáticamente. Si el problema continúa, el reinicio de la instancia de la base de datos o del servidor normalmente corrige el problema. Para obtener más información, busque el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de cada asociado para el error asociado que precedía a este mensaje.  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar la creación de reflejo de la base de datos &#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)  
  
  
