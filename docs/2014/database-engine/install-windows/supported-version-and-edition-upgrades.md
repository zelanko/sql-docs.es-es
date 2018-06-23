---
title: Actualizaciones de ediciones y versiones admitidas | Microsoft Docs
ms.custom: ''
ms.date: 10/26/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- components [SQL Server], adding to existing installations
- versions [SQL Server], upgrading
- upgrading SQL Server, upgrades supported
- cross-language support
ms.assetid: 702359c4-6ca9-42a8-860c-a95a802898a1
caps.latest.revision: 132
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: dc7140188a24ba8b8ca51b792d4dd2beb8384ce6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105689"
---
# <a name="supported-version-and-edition-upgrades"></a>Actualizaciones de ediciones y versiones admitidas
  Puede actualizar desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], y [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], y [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. En este tema se enumeran las formas de actualización admitidas desde estas versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y las actualizaciones de edición admitidas para [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
## <a name="pre-upgrade-checklist"></a>Lista de comprobación previa a la actualización  
  
-   Antes de actualizar una edición de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] , compruebe que las funciones que utiliza se admiten en la edición a la que desea moverse.  
  
-   Antes de actualizar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], habilite la autenticación de Windows para el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y compruebe la configuración predeterminada: la cuenta de servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ser miembro del grupo sysadmin de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Para actualizar a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], debe ejecutar un sistema operativo admitido. Para obtener más información, vea [Hardware and Software Requirements for Installing SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md).  
  
-   La actualización se bloqueará si hay un reinicio pendiente.  
  
-   La actualización se bloqueará si el servicio de Windows Installer no se está ejecutando.  
  
## <a name="unsupported-scenarios"></a>Escenarios no admitidos  
  
-   No se admiten instancias de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] de distintas versiones. Los números de versión de [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] deben ser los mismos en una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
-   No se admite la actualización entre plataformas. No puede actualizar una instancia de 32 bits de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a 64 bits nativo con el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Sin embargo, puede realizar copias de seguridad o separar bases de datos de una instancia de 32 bits de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y, después, si no están publicadas en replicación, restaurarlas o anexarlas a una nueva instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (64 bits). Debe volver a crear los inicios de sesión y los demás objetos de usuario en las bases de datos del sistema maestra, msdb y modelo.  
  
-   No puede agregar características nuevas durante la actualización de una instancia existente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Después de actualizar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], puede agregar características mediante el programa de instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obtener más información, consulte [agregar características a una instancia de SQL Server 2014 &#40;el programa de instalación&#41;](add-features-to-an-instance-of-sql-server-setup.md).  
  
-   Los clústeres de conmutación por error no se admiten en el modo WOW.  
  
-   La actualización de una edición de evaluación de una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se admite.  
  
## <a name="upgrades-from-earlier-versions-to-includesssql14includessssql14-mdmd"></a>Actualizaciones de versiones anteriores a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
> [!NOTE]  
>  La compatibilidad con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] se describe con más detalle en la próxima sección, 'Compatibilidad de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]'.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ediciones de 32 bits pueden actualizarse a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] en el subsistema de 32 bits (WOW64) de un servidor de 64 bits.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] las versiones de 64 bits pueden actualizarse a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] solo servidor de 64 bits.  
  
> [!NOTE]  
>  Al actualizar a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] desde una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Edition, elija entre “Enterprise Edition: Licencia Core” y “Enterprise Edition”. Estas ediciones Enterprise se diferencian solamente en los modos de licencia y el número máximo de núcleos admitidos. Para obtener más información, consulte [Compute Capacity Limits by Edition of SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md).  
  
 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] admite la actualización de las siguientes versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 o posterior  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 o posterior  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 o posterior  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 o posterior  
  
 En la siguiente tabla se indican los escenarios de actualización de versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]admitidos.  
  
|Actualización de|Ruta de actualización admitida|  
|------------------|----------------------------|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Enterprise|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Developer|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Desarrollador|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Standard|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Workgroup|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Express,<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Express with Tools y<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP4 Express con Advanced Services|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Enterprise|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Developer|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Desarrollador|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Standard|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Small Business|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Web|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Workgroup|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Express,<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Express with Tools y<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP3 Express con Advanced Services|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Datacenter|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Enterprise|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Developer|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Desarrollador|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Small Business|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Standard|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Web|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Workgroup|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Express,<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Express with Tools y<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP2 Express with Advanced Services|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Enterprise|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Developer|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Desarrollador|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Standard|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Web|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Express,<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Express with Tools y<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Express Management Studio y<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Express con Advanced Services|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express|  
|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1 Business Intelligence|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
  
### <a name="includesssql14includessssql14-mdmd-support-for-includessversion2005includesssversion2005-mdmd"></a>[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Compatibilidad con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]  
 En esta sección se explica la compatibilidad de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. En [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], podrá hacer lo siguiente:  
  
-   Actualizar una [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] instancia del motor de base de datos para [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ejecutando [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] el programa de instalación mediante la instalación del asistente o desde el símbolo del sistema.  
  
-   Adjuntar una base de datos de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] (archivos mdf/ldf) a la instancia de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] del motor de base de datos.  
  
-   Restaurar una base de datos de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] a la instancia de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] del motor de base de datos desde una copia de seguridad.  
  
-   Actualizar un paquete [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]. Ejecutar paquetes con actualización en contexto automática.  
  
-   Actualizar una [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ejecutando [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] el programa de instalación.  
  
-   Hacer copia de seguridad de un cubo de [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] y restaurarla en [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
-   Actualizar [!INCLUDE[ssRSversion2005](../../includes/ssrsversion2005-md.md)] a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ejecutando el programa de instalación de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
-   Conectarse a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]utilizando [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 2014.  
  
 Cuando una base de datos de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] se actualiza a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], el nivel de compatibilidad de la base de datos se cambia de 90 a 100. (En [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], los valores válidos para el nivel de compatibilidad de base de datos son 100, 110 y 120.) En el tema [Nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level) se explica cómo el cambio del nivel de compatibilidad puede afectar a las aplicaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Los escenarios no especificados en la lista anterior no se admiten, incluidos pero no limitados a lo siguiente:  
  
-   Instalar [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] en el mismo equipo (en paralelo).  
  
-   Usar una instancia de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] como miembro de la topología de replicación que incluye una instancia de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] .  
  
-   Configurar la creación de reflejo de la base de datos entre instancias de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
-   Hacer copia de seguridad del registro de transacciones con trasvase de registros entre instancias de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
-   Configurar servidores vinculados entre instancias de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] y [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
-   Administrar una instancia de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Management Studio.  
  
-   Adjuntar un cubo de [!INCLUDE[ssASversion2005](../../includes/ssasversion2005-md.md)] en [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Management Studio.  
  
-   Conectarse a [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Management Studio.  
  
-   Administrar un servicio de [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Management Studio.  
  
-   Compatibilidad con componentes personalizados de terceros de Integration Services de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , por ejemplo de ejecución y actualización.  
  
## <a name="includesssql14includessssql14-mdmd-edition-upgrade"></a>[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Actualización de edición  
 En la tabla siguiente se enumeran los escenarios de actualización de edición de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]admitidos.  
  
 Para obtener instrucciones paso a paso sobre cómo realizar una actualización de edición, vea [actualizar a una edición diferente de SQL Server 2014 &#40;el programa de instalación&#41;](upgrade-to-a-different-edition-of-sql-server-setup.md).  
  
|Actualización de|Actualización a|  
|------------------|----------------|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (Server+CAL y Core) <sup>2</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (licencia Server+CAL o Core)|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise Evaluation <sup>2</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (licencia Server+CAL o Core)<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Desarrollador<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> La actualización de Evaluation Enterprise (una edición gratuita) a cualquiera de las ediciones de pago se admite para las instalaciones independientes, pero no para las instalaciones en clúster.|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Estándar <sup>2</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (licencia Server+CAL o Core)|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Developer <sup>2</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (licencia Server+CAL o Core)<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (licencia Server+CAL o Core)<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express <sup>1</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (licencia Server+CAL o Core)<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Business Intelligence<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Desarrollador<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Standard<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Web|  
  
 Además, también puede realizar una actualización de edición entre [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (licencia Server+CAL) y [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (licencia Core):  
  
|Actualización de edición desde|Actualización de edición a|  
|--------------------------|------------------------|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (licencia Server+CAL) <sup>2</sup>|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (licencia Core)|  
|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (licencia Core)|[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Enterprise (licencia Server+CAL)|  
  
 <sup>1</sup> también se aplica a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express with Tools y [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Express con Advanced Services.  
  
 <sup>2</sup> cambio de edición de un [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] clúster de conmutación por error está limitado. Los escenarios siguientes no se admiten en los clústeres de conmutación por error de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] :  
  
-   SQL Server 2014 Enterprise a SQL Server 2014 Developer, Standard o Enterprise Evaluation.  
  
-   SQL Server 2014 Developer a SQL Server 2014 Standard o Enterprise Evaluation.  
  
-   SQL Server 2014 Standard a SQL Server 2014 Enterprise Evaluation.  
  
-   SQL Server 2014 Enterprise Evaluation a SQL Server 2014 Standard.  
  
## <a name="see-also"></a>Vea también  
 [Características compatibles con las ediciones de SQL Server 2014](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [Requisitos de hardware y Software para instalar SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)   
 [Actualizar a SQL Server 2014](upgrade-sql-server.md)   
 [Usar el Asesor de actualizaciones para preparar las actualizaciones](../../../2014/sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md)  
  
  
