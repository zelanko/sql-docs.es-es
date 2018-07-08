---
title: No compruebe que ningún archivo de base de datos en unidades comprimidas durante el proceso de actualización | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- compressed drives [SQL Server]
ms.assetid: 63be6853-c54a-42b2-ae1a-db2175f1d28e
caps.latest.revision: 19
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6adfb919f631a862dd896b70e41e462152c4ff47
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37198265"
---
# <a name="verify-that-no-database-files-are-on-compressed-drives-during-the-upgrade-process"></a>Comprobar que ningún archivo de base de datos se encuentre en unidades comprimidas durante el proceso de actualización
  El Asesor de actualizaciones ha detectado archivos de base de datos en una unidad comprimida. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede crear o actualizar las bases de datos en unidades comprimidas.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Acción correctora  
 Al instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], seleccione una unidad sin comprimir para las bases de datos del sistema y compruebe que las bases de datos que va a actualizar no están en unidades comprimidas. No obstante, tenga en cuenta que una vez actualizada la base de datos, puede colocar bases de datos de solo lectura y grupos de archivos secundarios de solo lectura en un sistema de archivos comprimidos NTFS.  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
