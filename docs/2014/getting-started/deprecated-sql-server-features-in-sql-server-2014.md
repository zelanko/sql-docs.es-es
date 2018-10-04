---
title: Características de SQL Server en SQL Server 2014 en desuso | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: fdc0c778-cc8d-42ab-8833-4deb4329f37a
author: mightypen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a90c1387a609ee59dec93b67e0a48bd2af7baf77
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48129775"
---
# <a name="deprecated-sql-server-features-in-sql-server-2014"></a>Características de SQL Server desusadas en SQL Server 2014
  En este tema se describen las características desusadas que siguen estando disponibles en [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Está previsto quitar estas características en una futura versión de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Las características en desuso no se deben usar en nuevas aplicaciones.  
  
## <a name="features-not-supported-in-the-next-version-of-includessnoversionincludesssnoversion-mdmd"></a>Características no admitidas en la siguiente versión de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
 Las características del [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] siguientes no se admitirán en la siguiente versión de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. No utilice estas características en nuevos trabajos de desarrollo y modifique lo antes posible las aplicaciones que las utilizan actualmente. La columna Nombre de característica aparece en eventos de seguimiento como ObjectName, en contadores de rendimiento y sys.dm_os_performance_counters como nombre_instancia. La columna Id. de característica aparece en eventos de seguimiento como ObjectId.  
  
|Categoría|Característica desusada|Sustituta|Nombre de característica|Id. de característica|  
|--------------|------------------------|-----------------|------------------|----------------|  
|Programación de datos|[Sys.soap_endpoints &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-soap-endpoints-transact-sql)|Windows Communications Foundation (WCF) o ASP.NET|Servicios web XML nativos|22|  
|Programación de datos|[Sys.endpoint_webmethods &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-endpoint-webmethods-transact-sql)|Windows Communications Foundation (WCF) o ASP.NET|Servicios web XML nativos|23|  
  
### <a name="slipstream-functionality"></a>Funcionalidad de instalación integrada  
 La característica Actualización del producto reemplaza a la funcionalidad de instalación integrada que estaba disponible en [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] PCU1. Por consiguiente, los parámetros de línea de comandos /*PCUSource* y /*CUSource*asociados a la funcionalidad de instalación integrada ya no deben usarse. Los parámetros continuarán funcionando, pero se pueden quitar en una versión futura del programa de instalación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. El parámetro /*UpdateSource* combina la funcionalidad de los parámetros de la instalación integrada, /*PCUSource* y /*CUSource*.  
  
 Para obtener más información acerca de la funcionalidad integrada que estaba disponible en [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] PCU1, vea [integrar una actualización de SQL Server](http://go.microsoft.com/fwlink/?LinkId=219945) (http://go.microsoft.com/fwlink/?LinkId=219945).  
  
## <a name="see-also"></a>Vea también  
 [Compatibilidad con versiones anteriores](../../2014/getting-started/backward-compatibility.md)  
  
  
