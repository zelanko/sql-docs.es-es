---
title: MSSQLSERVER_10001 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10001 (Database Engine error)
ms.assetid: f8fd2d8d-a4af-4b6a-ba51-9123b7e4c9bf
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 30e93a4b5794aa8f14722f2e331331766b209590
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85781579"
---
# <a name="mssqlserver_10001"></a>MSSQLSERVER_10001
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalles  
  
| Atributo | Value |  
| :-------- | :---- |  
|Nombre de producto|SQL Server|  
|Id. de evento|10001|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|HR_E_UNEXPECTED|  
|Texto del mensaje|El proveedor informó de un error grave inesperado.|  
  
## <a name="explanation"></a>Explicación  
El procesamiento de consultas distribuidas encontró un error genérico durante una llamada en el proveedor OLE DB.  
  
## <a name="user-action"></a>Acción del usuario  
Recopile eventos de seguimiento de OLE DB mediante [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] y proporcione estos datos al soporte técnico del producto para el proveedor OLE DB.  
  
## <a name="see-also"></a>Consulte también  
[Plantillas y permisos de SQL Server Profiler](~/tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)  
[SQL Server Native Client &#40;OLE DB&#41;](~/relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
