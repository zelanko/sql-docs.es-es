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
ms.openlocfilehash: 9061845efbbbf3c20b4d079af2c2b00cfeef1dfd
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "68068319"
---
# <a name="mssqlserver_10003"></a>MSSQLSERVER_10003
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|10003|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|HR_E_OUTOFMEMORY|  
|Texto del mensaje|Memoria insuficiente para el proveedor.|  
  
## <a name="explanation"></a>Explicación  
La escasa memoria del sistema ha hecho que el proveedor OLE DB se ejecute con memoria insuficiente.  
  
## <a name="user-action"></a>Acción del usuario  
Reinicie la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si esto apenas sirve, reinicie el equipo. Si el problema persiste, recopile eventos de seguimiento de OLE DB mediante [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] y proporcione estos datos al soporte técnico del producto para el proveedor OLE DB.  
  
## <a name="see-also"></a>Consulte también  
[Plantillas y permisos de SQL Server Profiler](~/tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)  
[SQL Server Native Client &#40;OLE DB&#41;](~/relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
