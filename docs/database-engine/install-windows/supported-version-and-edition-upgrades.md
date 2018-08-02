---
title: Actualizaciones de ediciones y versiones admitidas | Microsoft Docs
ms.custom: ''
ms.date: 06/27/2016
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: install
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- components [SQL Server], adding to existing installations
- versions [SQL Server], upgrading
- upgrading SQL Server, upgrades supported
- cross-language support
ms.assetid: 702359c4-6ca9-42a8-860c-a95a802898a1
caps.latest.revision: 148
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 163b52c2add9d6ea09d84d9d8b6b2f1e5171c1be
ms.sourcegitcommit: 8aa151e3280eb6372bf95fab63ecbab9dd3f2e5e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2018
ms.locfileid: "34770901"
---
# <a name="supported-version-and-edition-upgrades"></a>Actualizaciones de ediciones y versiones admitidas

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  
  Puede actualizar de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]y [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]. En este artículo se enumeran las formas de actualización admitidas desde estas versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y las actualizaciones de edición admitidas para [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)].  
  
## <a name="pre-upgrade-checklist"></a>Lista de comprobación previa a la actualización  
  
-   Antes de actualizar una edición de [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] , compruebe que las funciones que utiliza se admiten en la edición a la que desea moverse.  
  
-   Antes de actualizar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], habilite la autenticación de Windows para el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y compruebe la configuración predeterminada: la cuenta de servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ser miembro del grupo sysadmin de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Para actualizar a [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], debe ejecutar un sistema operativo admitido. Para más información, vea [Requisitos de hardware y software para instalar SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
-   La actualización se bloqueará si hay un reinicio pendiente.  
  
-   La actualización se bloqueará si el servicio de Windows Installer no se está ejecutando.  
  
## <a name="unsupported-scenarios"></a>Escenarios no admitidos  
  
-   No se admiten instancias de [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] de distintas versiones. Los números de versión de [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] deben ser los mismos en una instancia de [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)].  
  
-   [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] solo está disponible para plataformas de 64 bits. No se admite la actualización entre plataformas. No puede actualizar una instancia de 32 bits de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a 64 bits nativo con el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Sin embargo, puede realizar copias de seguridad o separar bases de datos de una instancia de 32 bits de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y, después, si no están publicadas en replicación, restaurarlas o anexarlas a una nueva instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (64 bits). Debe volver a crear los inicios de sesión y los demás objetos de usuario en las bases de datos del sistema maestra, msdb y modelo.  
  
-   No puede agregar características nuevas durante la actualización de una instancia existente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Después de actualizar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], puede agregar características mediante el programa de instalación de [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]. Para obtener más información, vea [Agregar características a una instancia de SQL Server 2016 &#40;programa de instalación&#41;](../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md).  
 
-   Los clústeres de conmutación por error no se admiten en el modo WOW.  
  
-   La actualización de una edición de evaluación de una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se admite.

-   Al actualizar desde RC1 o desde una versión anterior de SQL Server 2016 a RC3 o a una versión posterior, PolyBase debe desinstalarse antes de la actualización y reinstalarse tras ella.
  
## <a name="upgrades-from-earlier-versions-to-includesssql15-mdincludessssql15-mdmd"></a>Actualizaciones de versiones anteriores a [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]  
 
SQL Server 2016 admite la actualización de las siguientes versiones de SQL Server:
 
- [!INCLUDE[ssKatmai](../../includes/ssKatmai-md.md)] SP4 o posterior
- [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] SP3 o posterior
- [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 o posterior
- [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] o posterior 
 
> [!NOTE]  
> Para actualizar bases de datos en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] vea [Compatibilidad con la versión 2005](#SupportFor2005).  
  
En la siguiente tabla se indican los escenarios de actualización de versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]admitidos.  
  
|Actualización de|Ruta de actualización admitida|  
|------------------|----------------------------|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Enterprise|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Developer|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Desarrollador|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Standard|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Pequeña Empresa|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Web|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Workgroup|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP4 Express |[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Express|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Datacenter|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Enterprise|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Developer|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Desarrollador|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Pequeña Empresa|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Standard|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Web|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Workgroup|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP3 Express |[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Express|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Enterprise|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Developer|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Desarrollador <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Standard|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Web|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Express |[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Express <br/> <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Business Intelligence|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP2 Evaluation|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Evaluation <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Desarrollador|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Desarrollador|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Desarrollador <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express |[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Express <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Desarrollador|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/> |  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Evaluation|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Evaluation <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Desarrollador|  
|[!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] versión candidata para lanzamiento* |[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise |  
|[!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] Desarrollador |[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise | 

 \* La compatibilidad de Microsoft para actualizar del software de la versión candidata para lanzamiento está destinado específicamente a los clientes que han participado en el Programa de adopción de tecnología (TAP). 
   
###  <a name="SupportFor2005"></a> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Compatibilidad con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
En esta sección se explica la compatibilidad de [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. En [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], podrá hacer lo siguiente:  
  
-   Adjuntar una base de datos de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] (archivos mdf/ldf) a la instancia de [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] del motor de base de datos.  
  
-   Restaurar una base de datos de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] a la instancia de [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] del motor de base de datos desde una copia de seguridad.  
  
-   Hacer copia de seguridad de un cubo de [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] y restaurarla en [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)].  
  
> [!NOTE]  
> Cuando una base de datos de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] se actualiza a [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], el nivel de compatibilidad de la base de datos se cambia de 90 a 100. En [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)], los valores válidos del nivel de compatibilidad de la base de datos son 100, 110, 120 y 130. En el tema [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md) se explica cómo el cambio del nivel de compatibilidad puede afectar a las aplicaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Los escenarios no especificados en la lista anterior no se admiten, incluidos pero no limitados a lo siguiente:  
  
-   Instalar [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] en el mismo equipo (en paralelo).  
  
-   Usar una instancia de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] como miembro de la topología de replicación que incluye una instancia de [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] .  
  
-   Configurar la creación de reflejo de la base de datos entre instancias de [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] y [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
-   Hacer copia de seguridad del registro de transacciones con trasvase de registros entre instancias de [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] y [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
-   Configurar servidores vinculados entre instancias de [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] y [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
-   Administrar una instancia de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] desde [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Management Studio.  
  
-   Adjuntar un cubo de [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] en [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Management Studio.  
  
-   Conectarse a [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] desde [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Management Studio.  
  
-   Administrar un servicio de [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] desde [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Management Studio.  
  
-   Compatibilidad con componentes personalizados de terceros de Integration Services de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , por ejemplo de ejecución y actualización.  
  
## <a name="includesssql15-mdincludessssql15-mdmd-edition-upgrade"></a>[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Actualización de edición  
En la tabla siguiente se enumeran los escenarios de actualización de edición de [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]admitidos.  
  
Para obtener instrucciones paso a paso sobre cómo realizar una actualización de edición, vea [Actualizar a una edición diferente de SQL Server 2016 &#40;programa de instalación&#41;](../../database-engine/install-windows/upgrade-to-a-different-edition-of-sql-server-setup.md).  
  
|Actualización de|Actualización a|  
|------------------|----------------|  
|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (Server+CAL y Core)**|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise |  
|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Evaluation Enterprise**|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (licencia Server+CAL o Core) <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Desarrollador <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> La actualización de Evaluation (una edición gratuita) a cualquiera de las ediciones de pago se admite para las instalaciones independientes, pero no para las instalaciones en clúster.|  
|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard**|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (licencia Server+CAL o Core)|  
|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer**|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (licencia Server+CAL o Core) <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (licencia Server+CAL o Core) <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard|  
|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Express*|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (licencia Server+CAL o Core) <br/><br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Desarrollador <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard <br/> <br/> [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Web|  
  
Además, también puede realizar una actualización de edición entre [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (licencia Server+CAL) y [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (licencia Core):  
  
|Actualización de edición desde|Actualización de edición a|  
|--------------------------|------------------------|  
|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (licencia Server+CAL)**|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (licencia Core)|  
|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (licencia Core)|[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise (licencia Server+CAL)|  
  
 \* También se aplica a [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Express with Tools y [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Express con Advanced Services.  
  
 ** El cambio de edición de un clúster de conmutación por error de [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] está limitado. Los escenarios siguientes no se admiten en los clústeres de conmutación por error de [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] :  
  
-   [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Enterprise a [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer, Standard o Evaluation.  
  
-   [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Developer a [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard o Evaluation.  
  
-   [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard a [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Evaluation.  
  
-   [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Evaluation a [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] Standard.  
  
## <a name="see-also"></a>Ver también  

[Características compatibles con las ediciones de SQL Server 2016](../../sql-server/editions-and-supported-features-for-sql-server-2016.md)     
[Requisitos de hardware y software para instalar SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)     
[Actualizar a SQL Server 2016](../../database-engine/install-windows/upgrade-sql-server.md)    
  
  
