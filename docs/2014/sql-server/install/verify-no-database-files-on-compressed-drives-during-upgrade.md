---
title: Comprobar que no hay ningún archivo de base de datos en unidades comprimidas durante el proceso de actualización | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- compressed drives [SQL Server]
ms.assetid: 63be6853-c54a-42b2-ae1a-db2175f1d28e
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 9c04f7890ba8d8efe64afaf11b922af156c5de46
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065128"
---
# <a name="verify-that-no-database-files-are-on-compressed-drives-during-the-upgrade-process"></a>Comprobar que ningún archivo de base de datos se encuentre en unidades comprimidas durante el proceso de actualización
  El Asesor de actualizaciones ha detectado archivos de base de datos en una unidad comprimida. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede crear o actualizar las bases de datos en unidades comprimidas.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="corrective-action"></a>Acción correctora  
 Al instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], seleccione una unidad sin comprimir para las bases de datos del sistema y compruebe que las bases de datos que va a actualizar no están en unidades comprimidas. No obstante, tenga en cuenta que una vez actualizada la base de datos, puede colocar bases de datos de solo lectura y grupos de archivos secundarios de solo lectura en un sistema de archivos comprimidos NTFS.  
  
## <a name="see-also"></a>Consulte también  
 [Problemas de actualización Motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server el asesor de actualizaciones de 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
