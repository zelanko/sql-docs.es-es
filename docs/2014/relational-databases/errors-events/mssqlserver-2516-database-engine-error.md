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
ms.openlocfilehash: a963119e19bf1561d3d14bf11cdec3271af1ffb0
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/21/2020
ms.locfileid: "86552100"
---
# <a name="mssqlserver_2516"></a>MSSQLSERVER_2516
    
## <a name="details"></a>Detalles  
  
|Atributo|Value|  
|-|-|  
|Nombre de producto|SQL Server|  
|Id. de evento|2516|  
|Origen de eventos|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|DBCC_REPAIR_DIFF_MAP_INVALIDATED|  
|Texto del mensaje|La reparación ha invalidado el mapa de bits diferencial de la base de datos NAME. La cadena de la copia de seguridad diferencial está rota. Debe realizar una copia de seguridad completa de la base de datos para poder realizar una copia de seguridad diferencial.|  
  
## <a name="explanation"></a>Explicación  
 Este mensaje informativo se devuelve cuando se repara el error MSSQLEngine_2515.  
  
## <a name="user-action"></a>Acción del usuario  
 Realice una copia de seguridad completa de la base de datos.  
  
## <a name="see-also"></a>Consulte también  
 [Crear una copia de seguridad completa de base de datos &#40;SQL Server&#41;](../backup-restore/create-a-full-database-backup-sql-server.md)  
  
  
