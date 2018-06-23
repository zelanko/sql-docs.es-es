---
title: No se puede actualizar las bases de datos de solo lectura | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- database cannot be upgraded
ms.assetid: 27964211-ea30-4390-b791-dcf225fb9ae7
caps.latest.revision: 13
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 11f94ceed205d8984ed5a253e1d989211012f10f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36204345"
---
# <a name="read-only-databases-cannot-be-upgraded"></a>No se pueden actualizar bases de datos de solo lectura
  El Asesor de actualizaciones ha determinado que no se pueden actualizar algunas bases de datos de esta instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 Se ha detectado una base de datos de solo lectura. Para actualizarla, el programa de instalación debe poder escribir en ella.  
  
## <a name="corrective-action"></a>Acción correctora  
 Cuando nadie utiliza la base de datos, utilice la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el Administrador corporativo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], o la instrucción ALTER DATABASE para cambiar la base de datos de lectura y escritura. La instrucción siguiente cambia la base de datos al modo de lectura y escritura.  
  
```  
USE master;  
GO  
ALTER DATABASE <database name>  
SET READ_WRITE;  
GO  
```  
  
 Para obtener más información acerca de la instrucción ALTER DATABASE, vea el tema "ALTER DATABASE ([!INCLUDE[tsql](../../includes/tsql-md.md)])" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
