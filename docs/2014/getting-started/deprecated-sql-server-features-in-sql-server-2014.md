---
title: Características desusadas SQL Server en SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: fdc0c778-cc8d-42ab-8833-4deb4329f37a
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e9749c9df163280e52d691fbf6838196b9ae1e4b
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706992"
---
# <a name="deprecated-sql-server-features-in-sql-server-2014"></a>Características de SQL Server desusadas en SQL Server 2014
  En este tema se describen las características desusadas que siguen estando disponibles en [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Está previsto quitar estas características en una futura versión de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Las características en desuso no se deben usar en nuevas aplicaciones.  
  
## <a name="features-not-supported-in-the-next-version-of-ssnoversion"></a>Características no admitidas en la siguiente versión de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
 Las características del [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] siguientes no se admitirán en la siguiente versión de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. No utilice estas características en nuevos trabajos de desarrollo y modifique lo antes posible las aplicaciones que las utilizan actualmente. La columna Nombre de característica aparece en eventos de seguimiento como ObjectName, en contadores de rendimiento y sys.dm_os_performance_counters como nombre_instancia. La columna Id. de característica aparece en eventos de seguimiento como ObjectId.  
  
|Category|Característica desusada|Sustituta|Nombre de característica|Id. de la característica|  
|--------------|------------------------|-----------------|------------------|----------------|  
|Programación de datos|[Sys. soap_endpoints &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-soap-endpoints-transact-sql)|Windows Communications Foundation (WCF) o ASP.NET|Servicios web XML nativos|22|  
|Programación de datos|[Sys. endpoint_webmethods &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-endpoint-webmethods-transact-sql)|Windows Communications Foundation (WCF) o ASP.NET|Servicios web XML nativos|23|  
  
### <a name="slipstream-functionality"></a>Funcionalidad de instalación integrada  
 La [característica de actualización del producto](/previous-versions/sql/sql-server-2012/hh231670(v=sql.110)?redirectedfrom=MSDN) se presentó en SQL Server 2012 como una extensión de la funcionalidad de instalación integrada que estaba disponible en [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] PCU1. En SQL Server 2014, la característica actualización del producto es el método recomendado que se utiliza para integrar SQL Server. Por lo tanto, los parámetros de línea de comandos,/*PCUSource* y/*CUSource*, asociados a la funcionalidad de instalación original, ya no deben usarse. Estos parámetros seguirán funcionando, pero se pueden quitar en una versión futura del [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] programa de instalación. El parámetro recomendado que se va a usar es/*UpdateSource* , que combina la funcionalidad de los parámetros de instalación original,/*PCUSource* y/*CUSource*.  
  
 Para obtener más información sobre la funcionalidad de instalación integrada que estaba disponible en [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] PCU1, vea instalación [integrada de una actualización de SQL Server](https://go.microsoft.com/fwlink/?LinkId=219945) ( https://go.microsoft.com/fwlink/?LinkId=219945) .  
 Para obtener información sobre cómo usar/*UpdateSource* para integrar SQL Server compilaciones, consulte lo siguiente:
 
 - [Cómo aplicar una revisión SQL Server el programa de instalación de 2012 con un paquete de instalación actualizado (mediante UpdateSource para obtener una configuración inteligente)](https://blogs.msdn.microsoft.com/jason_howell/2012/08/28/how-to-patch-sql-server-2012-setup-with-an-updated-setup-package-using-updatesource-to-get-a-smart-setup/)
 
 - [SQL Server el programa de instalación de 2012 es más inteligente...](https://techcommunity.microsoft.com/t5/SQL-Server-Support/SQL-Server-2012-Setup-just-got-smarter-8230/ba-p/317440)
 
## <a name="see-also"></a>Consulte también  
 [Compatibilidad con versiones anteriores](../../2014/getting-started/backward-compatibility.md)  
  
  
