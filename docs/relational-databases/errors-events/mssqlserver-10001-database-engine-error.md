---
title: MSSQLSERVER_10001 | Microsoft Docs
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
- 10001 (Database Engine error)
ms.assetid: f8fd2d8d-a4af-4b6a-ba51-9123b7e4c9bf
caps.latest.revision: 16
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 571305890b3c5c8d879be2e4df5caa69cdc16e1b
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="mssqlserver10001"></a>MSSQLSERVER_10001
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|10001|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|HR_E_UNEXPECTED|  
|Texto del mensaje|El proveedor informó de un error grave inesperado.|  
  
## <a name="explanation"></a>Explicación  
El procesamiento de consultas distribuidas encontró un error genérico durante una llamada en el proveedor OLE DB.  
  
## <a name="user-action"></a>Acción del usuario  
Recopile eventos de seguimiento de OLE DB mediante [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] y proporcione estos datos al soporte técnico del producto para el proveedor OLE DB.  
  
## <a name="see-also"></a>Ver también  
[SQL Server Profiler Templates and Permissions](~/tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md) (Plantillas y permisos de SQL Server Profiler)  
[SQL Server Native Client &#40;OLE DB&#41;](~/relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
