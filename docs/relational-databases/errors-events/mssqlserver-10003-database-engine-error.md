---
title: MSSQLSERVER_10003 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10003 (Database Engine error)
ms.assetid: 9e2cb199-f077-4d88-8117-1b7550afc696
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 674a068985b3de4c89f85c1878344ef665cc0511
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63049054"
---
# <a name="mssqlserver10003"></a>MSSQLSERVER_10003
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|10003|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|HR_E_OUTOFMEMORY|  
|Texto del mensaje|Memoria insuficiente para el proveedor.|  
  
## <a name="explanation"></a>Explicación  
La escasa memoria del sistema ha hecho que el proveedor OLE DB se ejecute con memoria insuficiente.  
  
## <a name="user-action"></a>Acción del usuario  
Reinicie la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si esto apenas sirve, reinicie el equipo. Si el problema persiste, recopile eventos de seguimiento de OLE DB mediante [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] y proporcione estos datos al soporte técnico del producto para el proveedor OLE DB.  
  
## <a name="see-also"></a>Consulte también  
[SQL Server Profiler Templates and Permissions](~/tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md) (Plantillas y permisos de SQL Server Profiler)  
[SQL Server Native Client &#40;OLE DB&#41;](~/relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
