---
title: Características de herramientas de administración no incluidas en SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
ms.assetid: 6e58acd0-73c5-4161-9fbc-8ea531bc681c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7c966c3e4388588810438d7e91a9ae0356ef60c3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62780354"
---
# <a name="discontinued-management-tools-features-in-sql-server-2014"></a>Características de Herramientas de administración no incluidas en SQL Server 2014
  Este tema describe las características de Herramientas de administración de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que ya no están disponibles en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="features-removed-in-sscurrent"></a>Características eliminadas en [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]  
 None  
  
## <a name="features-removed-in-sssql11"></a>Características eliminadas en [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]  
  
### <a name="sql-server-compact-edition"></a>SQL Server Compact Edition  
 El editor de código de SQL Server Compact Edition se ha quitado de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. También se ha quitado la compatibilidad con SQL Server Compact Edition del Explorador de objetos, del Explorador de soluciones y del Explorador de plantillas. Utilice los editores de Transact-SQL en Microsoft Visual Studio 2010 Service Pack 1 o si no, de Webmatrix.  
  
### <a name="activex-subsystem-for-sql-server-agent"></a>Subsistema ActiveX para el Agente SQL Server  
 El subsistema ActiveX para el Agente SQL Server se ha quitado en esta versión. No existe ninguna funcionalidad que lo reemplace.  
  
### <a name="sp_addtask-sp_deletetask-sp_updatetask"></a>sp_addtask, sp_deletetask, sp_updatetask  
 Sp_addtask, el sp_deletetask y sp_updatetask se han quitado en esta versión. No utilice esta funcionalidad en aplicaciones nuevas o actualizadas.  
  
### <a name="net-send-and-pager-notification"></a>NET SEND y notificación mediante buscapersonas  
 NET SEND y notificación mediante buscapersonas se han quitado en esta versión. No utilice esta funcionalidad en aplicaciones nuevas o actualizadas.  
  
### <a name="data-tier-applications"></a>Aplicaciones de capa de datos  
 Algunas características de la aplicación de nivel de datos (DAC) presentes en [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] se han quitado de [!INCLUDE[ssSQL11](../includes/sssql11-md.md)]. Sin embargo, Data-Tier Application Framework (DACfx versión 3.0) que se publicó con [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] es compatible con [!INCLUDE[ssVersion2005](../includes/ssversion2005-md.md)] a través de [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] y de [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)]. DAC versión 3.0 no se admite en las versiones anteriores de [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] incluida [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] en [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)]. Los proyectos de base de datos de Visual Studio 2010 no admiten los paquetes DACPAC de DAC 3.0 o los paquetes de DAC Export (BACPAC) generados con DACfx versión 3.0 o posterior.  
  
 Microsoft recomienda usar la versión disponible más reciente de proyectos de base de datos de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools.  
  
 La API DACfx 3.0 y las herramientas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no permiten leer los archivos DACPAC y BACPAC creados con las herramientas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y las versiones de DACfx anteriores, extraer las bases de datos en archivos de DACPAC de estas versiones ni implementar las bases de datos en versiones admitidas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a través de [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Data Tools.  
  
## <a name="see-also"></a>Consulte también  
 [Compatibilidad con versiones anteriores](../../2014/getting-started/backward-compatibility.md)  
  
  
