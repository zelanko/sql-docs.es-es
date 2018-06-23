---
title: Cambios importantes a la administración de las características de SQL Server 2014 herramientas | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- tools-ssms
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 3ff3fad8-b569-4516-bd58-5a3efeb537e2
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 33e204958f9cea2db092f2a9c4b7d20648e4182c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112985"
---
# <a name="breaking-changes-to-management-tools-features-in-sql-server-2014"></a>Últimos cambios en las características de las herramientas de administración de SQL Server 2014
  En este tema se describen los últimos cambios realizados en las características de las herramientas de administración. Estos cambios pueden provocar errores en las aplicaciones, en los scripts o en las funcionalidades basados en versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Podría encontrar estos problemas al actualizar. Para obtener más información, vea [Use Upgrade Advisor to Prepare for Upgrades](../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md).  
  
## <a name="breaking-changes-in-includesssql14includessssql14-mdmd"></a>Principales cambios en [!INCLUDE[ssSQL14](../includes/sssql14-md.md)]  
 La información se proporcionará posteriormente.  
  
## <a name="breaking-changes-in-includesssql11includessssql11-mdmd"></a>Principales cambios en [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
  
### <a name="you-cannot-use-includesssql11includessssql11-mdmd-management-tools-to-create-a-utility-control-point-on-a-includesskilimanjaroincludessskilimanjaro-mdmd-instance-of-sql-server"></a>No puede utilizar las Herramientas de administración de [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] para crear un punto de control de la utilidad en una instancia de [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] de SQL Server  
 Para crear un punto de control de la utilidad en una instancia de [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)], utilice las herramientas de administración de [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] .  
  
### <a name="smo-has-been-reversioned-in-includesssql11includessssql11-mdmd"></a>Ha sido creado una nueva versión de SMO [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
 El código desarrollado con SMO de [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] o versiones anteriores podría no crearse en [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] sin tener que hacer modificaciones. Para más información, consulte [Backward Compatibility in SMO](../relational-databases/server-management-objects-smo/backward-compatibility-in-smo.md).  
  
## <a name="see-also"></a>Vea también  
 [Compatibilidad con versiones anteriores](../../2014/getting-started/backward-compatibility.md)  
  
  