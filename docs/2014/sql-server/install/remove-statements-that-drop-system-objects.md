---
title: Quitar instrucciones que quiten objetos del sistema | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- drop system objects [SQL Server]
ms.assetid: cdfc3c50-c801-4039-a4bf-b35f876f1c61
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 4c017e6fedbc7fd994e5b2d2ca4de184a082da65
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104843"
---
# <a name="remove-statements-that-drop-system-objects"></a>Quitar instrucciones que quiten objetos del sistema
  El Asesor de actualizaciones ha detectado instrucciones que quitan objetos del sistema. Los objetos del sistema, incluidos los procedimientos almacenados extendidos, se implementan en la base de datos de **recursos** de solo lectura (mssqlsystemresource) y no se pueden quitar. Modifique las aplicaciones para revocar o denegar el permiso EXECUTE en los objetos del sistema.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 Las instrucciones como DROP TABLE, DROP PROCEDURE y **sp_dropextendedproc** no se pueden utilizar para quitar objetos del sistema, porque estos objetos se implementan en la base de datos de solo lectura **resource** .  
  
## <a name="corrective-action"></a>Acción correctora  
 Quite  de las aplicaciones todas las instrucciones que intenten quitar objetos del sistema. Modifique las aplicaciones para revocar o denegar el permiso EXECUTE en los objetos del sistema. También puede utilizar la herramienta de configuración de área expuesta (SAC) para deshabilitar algunos de estos objetos. Por ejemplo, el procedimiento almacenado extendido **xp_cmdshell** se puede habilitar o deshabilitar utilizando la herramienta SAC.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
