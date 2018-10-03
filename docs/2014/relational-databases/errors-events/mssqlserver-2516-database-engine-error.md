---
title: MSSQLSERVER_2516 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 2516 (Database Engine error)
ms.assetid: 79ed14b5-f53c-40c6-8334-8a083f732207
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e88e90a56da7cb413c66da5f422b2b8f0d1abe91
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48135595"
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
 [Crear una copia de seguridad completa de base de datos &#40;SQL Server&#41;](../backup-restore/create-a-full-database-backup-sql-server.md)  
  
  
