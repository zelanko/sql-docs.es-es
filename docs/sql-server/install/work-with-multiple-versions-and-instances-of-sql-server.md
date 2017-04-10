---
title: "Trabajar con varias versiones e instancias de SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "instalaciones simultáneas [SQL Server]"
  - "versiones [SQL Server], varias"
  - "simultáneas, instalaciones [SQL Server]"
  - "varias versiones de componentes de SQL Server"
  - "instalar SQL Server, instalaciones en paralelo"
  - "instalación [SQL Server], instalaciones en paralelo"
  - "edición de 64 bits [SQL Server]"
  - "edición de 32 bits [SQL Server]"
  - "ediciones [SQL Server], instalaciones en paralelo"
ms.assetid: 93acefa8-bb41-4ccc-b763-7801f51134e0
caps.latest.revision: 67
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 67
---
# Trabajar con varias versiones e instancias de SQL Server
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite varias instancias de [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] en el mismo equipo. También puede actualizar las versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un equipo en el que ya estén instaladas versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para conocer escenarios de actualización admitidos, vea [Actualizaciones de ediciones y versiones admitidas](../../database-engine/install-windows/supported-version-and-edition-upgrades.md).  
  
## Componentes de versión y numeración  
 Los siguientes conceptos resultan útiles para entender el comportamiento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para instancias en paralelo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 El formato de versión de producto estándar para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es MM.nn.bbbb.rr, donde cada segmento se define del siguiente modo:  
  
 PP: versión principal  
  
 ss: versión secundaria  
  
 cccc: número de compilación  
  
 rr: número de revisión de la compilación  
  
 En cada lanzamiento principal o secundario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], hay un incremento del número de versión para diferenciarlo de las versiones anteriores. Este cambio de la versión se usa para numerosos propósitos. Entre otros, se incluye la presentación de información de la versión en la interfaz de usuario, el control del modo en que los archivos se reemplazan durante la actualización, la aplicación de Service Pack y también como un mecanismo para la diferenciación funcional entre las versiones sucesivas.  
  
### Componentes compartidos por todas las versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Determinados componentes se comparten en todas las instancias de todas las versiones instaladas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Al instalar diferentes versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en paralelo en el mismo equipo, estos componentes se actualizan automáticamente a la versión más reciente. Dichos componentes normalmente se desinstalan de forma automática cuando se desinstala la última instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Ejemplos: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser y Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VSS Writer.  
  
### Componentes compartidos por todas las instancias de la misma versión principal de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que tienen la misma versión principal comparten algunos componentes en todas las instancias. Si los componentes compartidos se seleccionan durante la actualización, los componentes existentes se actualizan a la última versión.  
  
 Ejemplos: [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]y Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### Componentes compartidos por las versiones secundarias  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que tienen la misma versión principal.secundaria comparten algunos componentes.  
  
 Ejemplo: archivos auxiliares para la instalación.  
  
### Componentes específicos de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Algunos componentes o servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] son específicos de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. También se denominan dependientes de la instancia. Comparten la misma versión que la instancia que los hospeda y se usan exclusivamente para dicha instancia.  
  
 Ejemplos: [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
### Componentes que son independientes de las versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Determinados componentes se instalan durante la instalación [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , pero son independientes de las versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se pueden compartir en las versiones principales o en todas las versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Ejemplos: Microsoft Sync Framework y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
 Para obtener más información sobre la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact, vea [Instalación de SQL Server 2016 desde el Asistente para la instalación &#40;programa de instalación&#41;](../../database-engine/install-windows/install-sql-server-2016-from-the-installation-wizard-setup.md). Para obtener más información sobre cómo desinstalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact, vea [Desinstalar una instancia existente de SQL Server &#40;programa de instalación&#41;](../../sql-server/install/uninstall-an-existing-instance-of-sql-server-setup.md).  
  
## Usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en paralelo con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Puede instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un equipo que ya ejecute instancias de una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si ya existe una instancia predeterminada en el equipo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se debe instalar como una instancia con nombre.  
  
> [!CAUTION]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no admite la instalación en paralelo de las instancias preparadas de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el mismo equipo. Por ejemplo, no puede preparar una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] en paralelo con una instancia preparada de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Sin embargo, puede instalar varias instancias preparadas de la misma versión principal de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en paralelo en el mismo equipo. Para más información, consulte [Considerations for Installing SQL Server Using SysPrep](../../database-engine/install-windows/considerations-for-installing-sql-server-using-sysprep.md).  
>   
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no se puede instalar en paralelo con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un equipo que ejecute Windows Server 2008 R2 Server Core SP1. Para obtener más información sobre cómo llevar a cabo una instalación Server Core, vea [Instalación de SQL Server 2016 en Server Core](../../database-engine/install-windows/install-sql-server-2016-on-server-core.md).  
  
 En la tabla siguiente se muestra la compatibilidad para las configuraciones en paralelo de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
|Instancia existente de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|Compatibilidad en paralelo|  
|--------------------------------------------------|----------------------------|  
|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (64 bits) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]|[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] (32 bits)<br /><br /> [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] (64 bits) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (32 bits)<br /><br /> [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (64 bits) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] (32 bits)<br /><br /> [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] (64 bits) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (32 bits)<br /><br /> [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (64 bits) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (32 bits)<br /><br /> [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] (64 bits) [!INCLUDE[vcprx64](../../includes/vcprx64-md.md)]|  
  
## Evitar conflictos de direcciones IP  
 Al instalar una instancia de clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en paralelo con una instancia independiente de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], tenga cuidado para evitar conflictos de número de puerto TCP en las direcciones IP. Los conflictos suelen suceder cuando se configuran dos instancias de [!INCLUDE[ssDE](../../includes/ssde-md.md)] para usar el puerto TCP (1433). Para evitar conflictos, configure una instancia para que utilice un puerto fijo predeterminado. La configuración de un puerto fijo es normalmente lo más sencillo en el caso de la instancia independiente. La configuración de [!INCLUDE[ssDE](../../includes/ssde-md.md)] para utilizar puertos diferentes evitará un conflicto inesperado entre el puerto TCP y la dirección IP que impide que se inicie la instancia cuando una instancia de clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] produce un error en el nodo en espera  
  
## Vea también  
 [Requisitos de hardware y software para instalar SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md)   
 [Instalación de SQL Server 2016 desde el Asistente para la instalación &#40;programa de instalación&#41;](../../database-engine/install-windows/install-sql-server-2016-from-the-installation-wizard-setup.md)   
 [Actualizaciones de ediciones y versiones admitidas](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)   
 [Actualizar a SQL Server 2016](../../database-engine/install-windows/upgrade-to-sql-server-2016.md)   
 [Características compatibles con las ediciones de SQL Server 2016](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)   
 [Compatibilidad con versiones anteriores](../Topic/Backward%20Compatibility_deleted.md)  
  
  