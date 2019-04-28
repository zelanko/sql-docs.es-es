---
title: Quite las instrucciones que modifican objetos del sistema | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- direct system catalog updates [SQL Server]
- system catalogs [SQL Server]
ms.assetid: 221b46c2-c27e-4df8-bd8c-8b990d6d5e98
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ebc7288bd7c72ce76df69d11c7a9fb0771764fca
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62856144"
---
# <a name="remove-statements-that-modify-system-objects"></a>Eliminar instrucciones que modifican objetos del sistema
  El Asesor de actualizaciones ha detectado la existencia de instrucciones que actualizan el catálogo del sistema. No se permite realizar actualizaciones directas del catálogo del sistema. Modifique los scripts de SQL para que utilicen API documentadas y oficiales.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 No se permite realizar actualizaciones directas del catálogo del sistema. Cualquier intento de hacerlo generará el siguiente error:  
  
 `Server: Msg 259, Level 16, State 1, Line 1`  
  
 `Ad hoc updates to system catalogs are not allowed.`  
  
## <a name="corrective-action"></a>Acción correctora  
 Modifique los scripts de SQL para que utilicen API documentadas y oficiales. Por ejemplo, utilice ALTER DATABASE *database_name* SET EMERGENCY en lugar de ejecutar una instrucción UPDATE en la tabla del sistema **sysdatabases** .  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
