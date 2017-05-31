---
title: MSSQLSERVER_10001 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 10001 (Database Engine error)
ms.assetid: f8fd2d8d-a4af-4b6a-ba51-9123b7e4c9bf
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 6db18eb8805eef626a72332bf6190c39fda97981
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver10001"></a>MSSQLSERVER_10001
  
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
  
## <a name="see-also"></a>Vea también  
[SQL Server Profiler Templates and Permissions](~/tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md) (Plantillas y permisos de SQL Server Profiler)  
[SQL Server Native Client &#40;OLE DB&#41;](~/relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  

