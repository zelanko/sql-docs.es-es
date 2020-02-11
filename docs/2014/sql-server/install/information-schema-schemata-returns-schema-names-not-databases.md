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
manager: craigg
ms.openlocfilehash: 0e3683ee043785ec6adc349ac52301280c7bc2b8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66094729"
---
# <a name="information_schemaschemata-returns-schema-names-in-a-database-not-databases-in-an-instance"></a>INFORMATION_SCHEMA.SCHEMATA devuelve los nombres de esquema en una base de datos, no las bases de datos en una instancia
  El Asesor de actualizaciones ha detectado instrucciones que hacen referencia a la vista INFORMATION_SCHEMA.SCHEMATA. En versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta vista devolvía todas las bases de datos de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y en versiones posteriores, la vista devuelve todos los esquemas de una base de datos.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
## <a name="description"></a>Descripción  
 En versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la vista INFORMATION_SCHEMA.SCHEMATA devolvía todas las bases de datos de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ahora, la vista devuelve todos los esquemas en una base de datos, lo cual cumple el estándar SQL.  
  
## <a name="corrective-action"></a>Acción correctora  
 Modifique la aplicación para que haga referencia a la vista de catálogo **Sys. Databases** para devolver todas las bases de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de una instancia de.  
  
## <a name="see-also"></a>Consulte también  
 [Problemas de actualización Motor de base de datos](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server el asesor de actualizaciones de 2014 &#91;nuevo&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
