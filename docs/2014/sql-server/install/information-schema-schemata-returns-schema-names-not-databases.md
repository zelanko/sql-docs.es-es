---
title: INFORMATION_SCHEMA. Esquemas devuelve los nombres de esquema en una base de datos, no en las bases de datos de una instancia | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- INFORMATION_SCHEMA.SCHEMATA view
ms.assetid: 4337b643-910d-47d7-bea8-f4052066b9a2
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: cb2a34a59bf6257c188210fc7bf2aeacb70f6b7f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85054796"
---
# <a name="information_schemaschemata-returns-schema-names-in-a-database-not-databases-in-an-instance"></a>INFORMATION_SCHEMA.SCHEMATA devuelve los nombres de esquema en una base de datos, no las bases de datos en una instancia
  El Asesor de actualizaciones ha detectado instrucciones que hacen referencia a la vista INFORMATION_SCHEMA.SCHEMATA. En versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta vista devolvía todas las bases de datos de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y en versiones posteriores, la vista devuelve todos los esquemas de una base de datos.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 En versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la vista INFORMATION_SCHEMA.SCHEMATA devolvía todas las bases de datos de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ahora, la vista devuelve todos los esquemas en una base de datos, lo cual cumple el estándar SQL.  
  
## <a name="corrective-action"></a>Acción correctora  
 Modifique la aplicación para que haga referencia a la vista de catálogo **Sys. Databases** para devolver todas las bases de datos de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte también  
 [Problemas de actualización Motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server el asesor de actualizaciones de 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
