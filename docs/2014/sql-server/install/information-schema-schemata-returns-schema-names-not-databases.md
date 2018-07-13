---
title: INFORMATION_SCHEMA. Nombres de esquema devuelve esquemas en una base de datos, no las bases de datos en una instancia | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- INFORMATION_SCHEMA.SCHEMATA view
ms.assetid: 4337b643-910d-47d7-bea8-f4052066b9a2
caps.latest.revision: 19
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c32683c6dc6aaa26079443d2ff4bc5d1f0994d76
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37198445"
---
# <a name="informationschemaschemata-returns-schema-names-in-a-database-not-databases-in-an-instance"></a>INFORMATION_SCHEMA.SCHEMATA devuelve los nombres de esquema en una base de datos, no las bases de datos en una instancia
  El Asesor de actualizaciones ha detectado instrucciones que hacen referencia a la vista INFORMATION_SCHEMA.SCHEMATA. En versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta vista devolvía todas las bases de datos de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y en versiones posteriores, la vista devuelve todos los esquemas de una base de datos.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 En versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la vista INFORMATION_SCHEMA.SCHEMATA devolvía todas las bases de datos de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ahora, la vista devuelve todos los esquemas en una base de datos, lo cual cumple el estándar SQL.  
  
## <a name="corrective-action"></a>Acción correctora  
 Modifique la aplicación para hacer referencia a la **sys.databases** para devolver todas las bases de datos en una instancia de la vista de catálogo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Problemas de actualización de motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Asesor de actualizaciones de SQL Server 2014 &#91;nuevo&#93;](/sql/2014/sql-server/install/sql-server-2014-upgrade-advisor)  
  
  
