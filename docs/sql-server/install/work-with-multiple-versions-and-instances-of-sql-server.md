---
title: Trabajar con varias versiones e instancias de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 08/25/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: install
ms.reviewer: ''
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- concurrent installations [SQL Server]
- versions [SQL Server], multiple
- side-by-side installations [SQL Server]
- multiple SQL Server component versions
- installing SQL Server, side-by-side installations
- Setup [SQL Server], side-by-side installations
- 64-bit edition [SQL Server]
- 32-bit edition [SQL Server]
- editions [SQL Server], side-by-side installations
ms.assetid: 93acefa8-bb41-4ccc-b763-7801f51134e0
caps.latest.revision: 67
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 0e2d76ecc7b0c0f6be29f97dd0a6edc941b9d016
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="work-with-multiple-versions-and-instances-of-sql-server"></a>Trabajar con varias versiones e instancias de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite varias instancias de [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en el mismo equipo. También puede actualizar las versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un equipo en el que ya estén instaladas versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para conocer escenarios de actualización admitidos, vea [Actualizaciones de ediciones y versiones admitidas](../../database-engine/install-windows/supported-version-and-edition-upgrades.md).  
  
## <a name="version-components-and-numbering"></a>Componentes de versión y numeración  
 Los siguientes conceptos resultan útiles para entender el comportamiento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para instancias en paralelo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 El formato de versión de producto estándar para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es MM.nn.bbbb.rr, donde cada segmento se define del siguiente modo:  
  
 PP: versión principal  
  
 ss: versión secundaria  
  
 cccc: número de compilación  
  
 rr: número de revisión de la compilación  
  
 En cada lanzamiento principal o secundario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], hay un incremento del número de versión para diferenciarlo de las versiones anteriores. Este cambio de la versión se usa para numerosos propósitos. Entre otros, se incluye la presentación de información de la versión en la interfaz de usuario, el control del modo en que los archivos se reemplazan durante la actualización, la aplicación de Service Pack y también como un mecanismo para la diferenciación funcional entre las versiones sucesivas.  
  
### <a name="components-shared-by-all-versions-of-includessnoversionincludesssnoversion-mdmd"></a>Componentes compartidos por todas las versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Determinados componentes se comparten en todas las instancias de todas las versiones instaladas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Al instalar diferentes versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en paralelo en el mismo equipo, estos componentes se actualizan automáticamente a la versión más reciente. Dichos componentes normalmente se desinstalan de forma automática cuando se desinstala la última instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Ejemplos: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser y Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VSS Writer.  
  
### <a name="components-shared-across-all-instances-of-the-same-major-version-of-includessnoversionincludesssnoversion-mdmd"></a>Componentes compartidos por todas las instancias de la misma versión principal de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que tienen la misma versión principal comparten algunos componentes en todas las instancias. Si los componentes compartidos se seleccionan durante la actualización, los componentes existentes se actualizan a la última versión.  
  
 Ejemplos: [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]y Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="components-shared-across-minor-versions"></a>Componentes compartidos por las versiones secundarias  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que tienen la misma versión principal.secundaria comparten algunos componentes.  
  
 Ejemplo: archivos auxiliares para la instalación.  
  
### <a name="components-specific-to-an-instance-of-includessnoversionincludesssnoversion-mdmd"></a>Componentes específicos de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Algunos componentes o servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] son específicos de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. También se denominan dependientes de la instancia. Comparten la misma versión que la instancia que los hospeda y se usan exclusivamente para dicha instancia.  
  
 Ejemplos: [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
### <a name="components-that-are-independent-of-the-includessnoversionincludesssnoversion-mdmd-versions"></a>Componentes que son independientes de las versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Determinados componentes se instalan durante la instalación [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , pero son independientes de las versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se pueden compartir en las versiones principales o en todas las versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Ejemplos: Microsoft Sync Framework y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
 Para obtener más información sobre la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact, vea [Instalación de SQL Server 2016 desde el Asistente para la instalación &#40;programa de instalación&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md). Para obtener más información sobre cómo desinstalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact, vea [Desinstalar una instancia existente de SQL Server &#40;programa de instalación&#41;](../../sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md).  
  
## <a name="using-includessnoversionincludesssnoversion-mdmd-side-by-side-with-previous-versions-of-includessnoversionincludesssnoversion-mdmd"></a>Usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en paralelo con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Puede instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un equipo que ya ejecute instancias de una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si ya existe una instancia predeterminada en el equipo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se debe instalar como una instancia con nombre.  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no admite la instalación en paralelo de las instancias preparadas de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el mismo equipo. Por ejemplo, no puede preparar una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] en paralelo con una instancia preparada de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Sin embargo, puede instalar varias instancias preparadas de la misma versión principal de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en paralelo en el mismo equipo. Para más información, consulte [Considerations for Installing SQL Server Using SysPrep](../../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md).  
>   
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no se puede instalar en paralelo con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un equipo que ejecute Windows Server 2008 R2 Server Core SP1. Para obtener más información sobre cómo llevar a cabo una instalación Server Core, vea [Instalación de SQL Server 2016 en Server Core](../../database-engine/install-windows/install-sql-server-on-server-core.md).  
  
En la tabla siguiente se muestra la compatibilidad para las configuraciones en paralelo de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
|Instancia existente de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|Compatibilidad en paralelo|  
|--------------------------------------------------|----------------------------|  
|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (64 bits) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] (32 bits)<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] (64 bits) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (32 bits)<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (64 bits) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] (32 bits)<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] (64 bits) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (32 bits)<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (64 bits) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (32 bits)<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (64 bits) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)] <br /><br /> [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|  

En la tabla siguiente se muestra la compatibilidad en paralelo de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] con versiones anteriores:  
  
|Instancia existente de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|Compatibilidad en paralelo con versiones anteriores|  
|--------------------------------------------------|----------------------------|  
|[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] (32 bits)<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] (64 bits) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (32 bits)<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (64 bits) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] (32 bits)<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] (64 bits) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (32 bits)<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (64 bits) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (32 bits)<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (64 bits) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]|  

  
## <a name="preventing-ip-address-conflicts"></a>Evitar conflictos de direcciones IP  
 Al instalar una instancia de clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en paralelo con una instancia independiente de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], tenga cuidado para evitar conflictos de número de puerto TCP en las direcciones IP. Los conflictos suelen suceder cuando se configuran dos instancias de [!INCLUDE[ssDE](../../includes/ssde-md.md)] para usar el puerto TCP (1433). Para evitar conflictos, configure una instancia para que utilice un puerto fijo predeterminado. La configuración de un puerto fijo es normalmente lo más sencillo en el caso de la instancia independiente. La configuración de [!INCLUDE[ssDE](../../includes/ssde-md.md)] para utilizar puertos diferentes evitará un conflicto inesperado entre el puerto TCP y la dirección IP que impide que se inicie la instancia cuando una instancia de clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] produce un error en el nodo en espera  
  
## <a name="see-also"></a>Ver también  
 [Requisitos de hardware y software para instalar SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)   
 [Instalación de SQL Server desde el asistente para instalación](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)   
 [Actualizaciones de ediciones y versiones admitidas](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)   
 [Actualizar SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)   
 [Ediciones y características admitidas de SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md)   
 [Ediciones y características admitidas de SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md)   
 [Compatibilidad con versiones anteriores](http://msdn.microsoft.com/library/15d9117e-e2fa-4985-99ea-66a117c1e9fd)  
  
  
