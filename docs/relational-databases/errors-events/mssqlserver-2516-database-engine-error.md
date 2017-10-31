---
title: MSSQLSERVER_2516 | Microsoft Docs
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
- 2516 (Database Engine error)
ms.assetid: 79ed14b5-f53c-40c6-8334-8a083f732207
caps.latest.revision: 19
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: c8ccf3ec56b38fa53290531aac17e966a23a5a8d
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver2516"></a>MSSQLSERVER_2516
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|2516|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC_REPAIR_DIFF_MAP_INVALIDATED|  
|Texto del mensaje|La reparación ha invalidado el mapa de bits diferencial de la base de datos NAME. La cadena de la copia de seguridad diferencial está rota. Debe realizar una copia de seguridad completa de la base de datos para poder realizar una copia de seguridad diferencial.|  
  
## <a name="explanation"></a>Explicación  
Este mensaje informativo se devuelve cuando se repara el error MSSQLEngine_2515.  
  
## <a name="user-action"></a>Acción del usuario  
Realice una copia de seguridad completa de la base de datos.  
  
## <a name="see-also"></a>Vea también  
[Crear una copia de seguridad completa de base de datos &#40;SQL Server&#41;](~/relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  

