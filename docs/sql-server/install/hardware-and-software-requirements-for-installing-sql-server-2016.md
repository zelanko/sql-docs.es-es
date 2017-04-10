---
title: "Requisitos de hardware y software para instalar SQL Server 2016 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Programa de instalación [SQL Server], software"
  - "software [SQL Server]"
  - "instalación de SQL Server, software"
  - "sistemas operativos [SQL Server], requisitos de SQL Server"
  - "Programa de instalación [SQL Server], compatibilidad entre idiomas"
  - "sistemas operativos [SQL Server], compatibilidad entre idiomas"
  - "conexiones de red [SQL Server], requisitos"
  - "espacio en disco [SQL Server], instalaciones de SQL Server"
  - "WOW [SQL Server]"
  - "Programa de instalación [SQL Server], hardware"
  - "dependencias [SQL Server], instalaciones de SQL Server"
  - "requisitos de hardware de clúster [SQL Server]"
  - "extremos [SQL Server], instalaciones de SQL Server"
  - "Internet [SQL Server], instalaciones de SQL Server"
  - "hardware [SQL Server]"
  - "Windows en Windows [SQL Server]"
  - "instalación de SQL Server, hardware"
  - "Comprobador de configuración de instalación"
  - "SCC [SQL Server]"
  - "sistemas operativos [SQL Server]"
  - "espacio [SQL Server], instalaciones de SQL Server"
  - "comprobador de configuración del sistema"
  - "instalación de SQL Server, compatibilidad entre idiomas"
  - "Internet [SQL Server]"
  - "espacio [SQL Server]"
  - "compatibilidad con sistemas extendidos [SQL Server]"
  - "edición de 64 bits [SQL Server]"
  - "clústeres de conmutación por error [SQL Server]"
  - "clústeres de conmutación por error [SQL Server], requisitos de hardware"
  - "edición de 32 bits [SQL Server]"
  - "configuraciones regionales [SQL Server], instalaciones de SQL Server"
  - "compatibilidad entre idiomas"
  - "espacio de disco [SQL Server]"
  - "versiones de SQL Server traducidas"
ms.assetid: 09bcf20b-0a40-4131-907f-b61479d5e4d8
caps.latest.revision: 333
ms.author: "mikeray"
manager: "jhubbard"
---
# Requisitos de hardware y software para instalar SQL Server 2016
  En este tema se enumeran los requisitos mínimos de hardware y software para instalar y ejecutar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 **Pruébelo:**  
  
-   Descargue SQL Server desde el [**Centro de evaluación**.](https://www.microsoft.com/en-us/evalcenter/evaluate-sql-server-2016) 
  
-    Ponga en marcha una máquina virtual con [**SQL Server 2016**](https://azure.microsoft.com/en-us/marketplace/partners/microsoft/sqlserver2016rtmenterprisewindowsserver2012r2/?wt.mc_id=sqL16_vm) ya instalado.  
  
 **Las siguientes consideraciones son válidas para todas las ediciones:**  
  
-   Se recomienda ejecutar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] en equipos con los formatos de archivo NTFS o ReFS. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] se puede instalar en un equipo con el sistema de archivos FAT32, pero no se recomienda porque es menos seguro que el sistema de archivos NTFS o ReFS.  
  
-   El programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bloqueará las instalaciones en unidades de disco de solo lectura, asignadas o comprimidas.  
  
-   La instalación no se lleva a cabo si el programa de instalación se inicia a través de una Conexión a Escritorio remoto con los medios de un recurso local en el cliente RDC. Para realizar la instalación de forma remota, los medios deben estar en un recurso compartido de red o localmente en una máquina virtual o física. Los medios de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden estar en un recurso compartido de red, en una unidad asignada, en una unidad local o como una imagen ISO de una máquina virtual.  
  
-   Un requisito previo de la instalación de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] es tener instalado .NET 4.6.1. El programa de instalación instalará automáticamente .NET 4.6.1 cuando se seleccione [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
-   El programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala los siguientes componentes de software que el producto necesita:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client  
  
    -   Archivos auxiliares del programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   Para conocer los requisitos mínimos de versión para instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en [!INCLUDE[win8srv](../../includes/win8srv-md.md)] o [!INCLUDE[win8](../../includes/win8-md.md)], vea [Instalar SQL Server en Windows Server 2012 o Windows 8](http://support.microsoft.com/kb/2681562) (http://support.microsoft.com/kb/2681562).  
  
 Este tema contiene las siguientes secciones:  
  
-   [Requisitos de hardware y software](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md#hwswr)  
  
-   [Requisitos de procesador, memoria y sistema operativo](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md#pmosr)  
  
-   [Compatibilidad entre idiomas](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md#CrossLanguageSupport)  
  
-   [Requisitos de espacio en disco duro](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md#HardDiskSpace)  
  
-   [Tipos de almacenamiento para los archivos de datos](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md#StorageTypes)  
  
-   [Instalación de SQL Server en un controlador de dominio](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md#DC_support)  
  
##  <a name="a-namehwswra-hardware-and-software-requirements"></a><a name="hwswr"></a> Requisitos de hardware y software  
 Los siguientes requisitos se aplican a todas las instalaciones:  
  
|Componente|Requisito|  
|---------------|-----------------|  
|.NET Framework|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] RC1 y las versiones posteriores necesitan [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.6 para el Motor de base de datos, Master Data Services o la replicación. El programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2016 instala automáticamente [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] también se puede instalar manualmente desde [Microsoft .NET Framework 4.6 (instalador web) para Windows](http://support.microsoft.com/kb/3045560).<br/><br/> Para ver más información, recomendaciones y directrices sobre [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.6, consulte la [Guía de implementación de .NET Framework para desarrolladores](http://msdn.microsoft.com/library/ee942965\(v=vs.110\).aspx).<br/><br/>[!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)] y [!INCLUDE[winblue_server_2](../../includes/winblue-server-2-md.md)] necesitan [KB2919355](http://support.microsoft.com/kb/2919355) para instalar [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.6.|  
|Software de red|Los sistemas operativos admitidos para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tienen software de red integrado. Las instancias con nombre y predeterminadas de una instalación independiente admiten los siguientes protocolos de red: Memoria compartida, Canalizaciones con nombre, TCP/IP y VIA.<br/><br/> Nota: la memoria compartida y VIA no se admiten en clústeres de conmutación por error.<br/><br/> Además, el protocolo VIA está en desuso. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]<br/><br/> <br/><br/> Para obtener más información acerca de los protocolos de red y las bibliotecas de red, vea [Network Protocols and Network Libraries](../../sql-server/install/network-protocols-and-network-libraries.md).|  
|Disco duro|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] requiere un mínimo de 6 GB de espacio disponible en disco.<br/><br/> Las necesidades de espacio en disco variarán según los componentes de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] que instale. Para obtener más información, vea [Requisitos de espacio en disco duro](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md#HardDiskSpace), más adelante en este tema. Para obtener información acerca de los tipos de almacenamiento admitidos para los archivos de datos, vea [Storage Types for Data Files](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md#StorageTypes)|  
|Unidad|Para la instalación desde disco se necesita una unidad de DVD.|  
|Monitor|[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] requiere Super VGA (800x600) o un monitor de una resolución mayor.|  
|Internet|La funcionalidad de Internet necesita acceso a Internet (no necesariamente de carácter gratuito).|  
  
 Nota: la ejecución de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] en una máquina virtual será más lenta que la ejecución nativa, dada la sobrecarga de virtualización.  
  
 Existen otros requisitos de hardware y software para la característica PolyBase. Para obtener más información, vea [Introducción a PolyBase](../../relational-databases/polybase/get-started-with-polybase.md).  
  
##  <a name="a-namepmosra-processor-memory-and-operating-system-requirements"></a><a name="pmosr"></a> Requisitos de procesador, memoria y sistema operativo  
 Los siguientes requisitos de memoria y procesador se aplican a todas las ediciones de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
|Componente|Requisito|  
|---------------|-----------------|  
|Memoria*|**Mínimo:**<br/><br/> Ediciones Express: 512 MB<br/><br/> Todas las demás ediciones: 1 GB<br/><br/> **Recomendado:**<br/><br/> Ediciones Express: 1 GB<br/><br/> Todas las demás ediciones: al menos 4 GB y debe aumentar a medida que el tamaño de la base de datos aumente para asegurar un rendimiento óptimo.|  
|Velocidad del procesador|**Mínimo:** Procesador x64: 1,4 GHz<br/><br/> **Recomendado:** 2 GHz o más|  
|Tipo de procesador|Procesador x64: AMD Opteron, AMD Athlon 64, Intel Xeon compatible con Intel EM64T Intel Pentium IV compatible con EM64T|  
  
> [!NOTE]  
>  La instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] es posible únicamente en procesadores x64. Ya no es viable en procesadores x86.  
  
 La memoria mínima necesaria para instalar el componente [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] en [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) es 2 GB de RAM, que es diferente del requisito de memoria mínima de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obtener información acerca de cómo instalar DQS, vea [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md).  
  
 **Compatibilidad con WOW64:**  
  
 WOW64 ((Windows de 32 bits sobre Windows de 64 bits) es una característica de las ediciones de 64 bits de Windows que permite que las aplicaciones de 32 bits se ejecuten de forma nativa en el modo de 32 bits. Las aplicaciones funcionan en el modo de 32 bits, aunque el sistema operativo subyacente sea de 64 bits. WOW64 no se admite en instalaciones de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . Sin embargo, las Herramientas de administración sí se admiten en WOW64.  
  
 **Compatibilidad con el sistema operativo:**  
  
 Las ediciones de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] se clasifican en lo siguiente:  
  
-   [Ediciones principales de SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md#TOP_Principal)  
  
-   [Ediciones de amplio uso de SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md#TOP_Breadth)  
  
> [!NOTE]  
>  Dos excepciones a la compatibilidad de sistema operativo indicada en esta sección son las siguientes características de Business Intelligence, que se pueden instalar en Windows Server 2008 R2 SP1 o posterior:  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] - SharePoint  
  
-   Complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para productos de SharePoint  
  
### <a name="features-supported-on-32-bit-client-operating-systems"></a>Características admitidas en sistemas operativos de cliente de 32 bits  
 Los sistemas operativos de cliente de Windows, como Windows 10 y Windows 8.1, están disponibles en arquitecturas tanto de 32 bits como de 64 bits.   Los sistemas operativos de cliente de 64 bits admiten todas las características de SQL Server. En cuanto a los sistemas operativos de cliente de 32 bits compatibles, Microsoft admite las siguientes características:  
  
-   Cliente de calidad de datos  
  
-   Conectividad con las herramientas de cliente  
  
-   Integration Services  
  
-   Compatibilidad con versiones anteriores de las herramientas de cliente  
  
-   SDK de las herramientas de cliente  
  
-   Componentes de documentación  
  
-   Componentes de Distributed Replay  
  
-   Distributed Replay Controller  
  
-   Distributed Replay Client  
  
-   SDK de conectividad de cliente SQL  
  
 [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] y los sistemas operativos de servidor posteriores no están disponibles en arquitecturas de 32 bits. Todos los sistemas operativos de servidor admitidos están disponibles únicamente en 64 bits. Los sistemas operativos de servidor de 64 bits admiten todas las características.  
  
###  <a name="a-nametopprincipala-principal-editions-of-includesscurrenttokensscurrentmdmd"></a><a name="TOP_Principal"></a> Ediciones principales de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 La tabla siguiente se muestran los requisitos del sistema operativo para las ediciones principales de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
|Edición de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Sistema operativo compatible|  
|---------------------------------------|--------------------------------|  
|[!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)]|[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation|  
|[!INCLUDE[ssStandard](../../includes/ssstandard-md.md)]|[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation<br/><br/> Windows 10 Home<br/><br/> Windows 10 Professional<br/><br/> Windows 10 Enterprise<br/><br/>[!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]<br/><br/>[!INCLUDE[win8](../../includes/win8-md.md)]<br/><br/>[!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]<br/><br/>[!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]|  
|[!INCLUDE[ssWeb](../../includes/ssweb-md.md)]|[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation|  
  
###  <a name="a-nametopbreadtha-breadth-editions-of-includesscurrenttokensscurrentmdmd"></a><a name="TOP_Breadth"></a> Ediciones de amplio uso de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 La tabla siguiente se muestran los requisitos del sistema operativo para las ediciones de amplio uso de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
|Edición de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Sistema operativo compatible|  
|---------------------------------------|--------------------------------|  
|[!INCLUDE[ssDeveloper](../../includes/ssdeveloper-md.md)]|[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation<br/><br/> Windows 10 Home<br/><br/> Windows 10 Professional<br/><br/> Windows 10 Enterprise<br/><br/>[!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]<br/><br/>[!INCLUDE[win8](../../includes/win8-md.md)]<br/><br/>[!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]<br/><br/>[!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]|  
|[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]|[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation<br/><br/> Windows 10 Home<br/><br/> Windows 10 Professional<br/><br/> Windows 10 Enterprise<br/><br/>[!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]<br/><br/>[!INCLUDE[win8](../../includes/win8-md.md)]<br/><br/>[!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]<br/><br/>[!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]|  
  
##  <a name="a-namecrosslanguagesupporta-cross-language-support"></a><a name="CrossLanguageSupport"></a> Compatibilidad entre idiomas  
 Para más información sobre la compatibilidad entre idiomas y consideraciones sobre la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en idiomas localizados, consulte [Versiones en idioma local en SQL Server](../../sql-server/install/local-language-versions-in-sql-server.md).  
  
##  <a name="a-nameharddiskspacea-hard-disk-space-requirements"></a><a name="HardDiskSpace"></a> Requisitos de espacio en disco duro  
 Durante la instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], Windows Installer crea archivos temporales en la unidad del sistema. Antes de ejecutar el programa de instalación para instalar o actualizar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], compruebe que dispone de al menos 6,0 GB de espacio en disco en la unidad del sistema para estos archivos. Este requisito es aplicable incluso si instala todos los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en una unidad distinta de la predeterminada.  
  
 Los requisitos reales de disco duro dependen de la configuración del sistema y de las características que decida instalar. En la tabla siguiente se muestran los requisitos de espacio en disco de los componentes de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] :  
  
|**Característica**|**Requisito de espacio en disco**|  
|-----------------|--------------------------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] y archivos de datos, replicación, búsqueda de texto completo y Data Quality Services|1480 MB|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] (como arriba) con R Services (In-Database)|2744 MB|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] (como arriba) con Servicio de consultas de PolyBase para datos externos|4194 MB|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y archivos de datos|698 MB|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|967 MB|  
|[!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)] (independiente)|280 MB|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] - SharePoint|1203 MB|  
|Complemento [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para productos de SharePoint|325 MB|  
|[!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]|121 MB|  
|Conectividad con las herramientas de cliente|328 MB|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|306 MB|  
|Componentes de cliente (excepto los componentes de los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y las herramientas de Integration Services)|445 MB|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|280 MB|  
|Componentes de Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ver y administrar el contenido de la Ayuda*|27 MB|  
|Todas las características|8030 MB|  
  
 *Los requisitos de espacio en disco para el contenido descargado de los Libros en pantalla son 200 MB.  
  
##  <a name="a-namestoragetypesa-storage-types-for-data-files"></a><a name="StorageTypes"></a> Tipos de almacenamiento para los archivos de datos  
 Los tipos admitidos de almacenamiento para los archivos de datos son:  
  
-   Disco local  
  
-   Almacenamiento compartido  
  
-   Recurso compartido de archivos SMB  
  
    > [!NOTE]  
    >  El almacenamiento SMB no se admite para los archivos de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en instalaciones independientes o en clúster. Use almacenamiento de conexión directa o una red de área de almacenamiento en su lugar.  
  
    > [!IMPORTANT]  
    >  El almacenamiento SMB podría estar hospedado en un servidor de archivos Windows o en un dispositivo de almacenamiento SMB de terceros. Si se utiliza un servidor de archivos Windows, la versión de Windows File Server debería ser 2008 o posterior. Para obtener más información sobre la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante un recurso compartido de archivos SMB como opción de almacenamiento, vea [Install SQL Server with SMB Fileshare as a Storage Option](../../database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option.md).  
  
    > [!WARNING]  
    > La instalación de clústeres de conmutación por error de  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite el disco local solo para instalar los archivos tempdb. Asegúrese de que la ruta de acceso especificada para los archivos de datos y registro de tempdb es válida en todos los nodos del clúster. Durante la conmutación por error, si los directorios de tempdb no están disponibles en el nodo de destino de la conmutación por error, el recurso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no podrá ponerse en línea.  
  
##  <a name="a-namedcsupporta-installing-includessnoversiontokenssnoversionmdmd-on-a-domain-controller"></a><a name="DC_support"></a> Instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un controlador de dominio  
 Por razones de seguridad, se recomienda que no se instale [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] en un controlador de dominio. El programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no bloqueará la instalación en un equipo que sea un controlador de dominio, pero se aplican las limitaciones siguientes:  
  
-   No puede ejecutar los servicios [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un controlador de dominio bajo una cuenta del servicio local.  
  
-   Una vez instalado en un equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , no puede cambiar el equipo de un miembro de dominio a un controlador de dominio. Debe desinstalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de cambiar el equipo host a un controlador de dominio.  
  
-   Una vez instalado en un equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , no puede cambiar el equipo de un controlador de dominio a un miembro de dominio. Debe desinstalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de cambiar el equipo host a un miembro de dominio.  
  
-   Las instancias del clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se admiten si los nodos de clúster son controladores de dominio.  
  
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se admite en un controlador de dominio de solo lectura. El programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede crear grupos de seguridad ni suministrar cuentas de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un controlador de dominio de solo lectura. En este escenario, se producirá un error de instalación.  

- Una instancia de clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se admite en un entorno donde solo se puede obtener acceso a un controlador de dominio de solo lectura. 
  
## <a name="see-also"></a>Vea también  
 [Planear una instalación de SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Consideraciones de seguridad para una instalación de SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)   
 [Especificaciones de producto de SQL Server 2016](../Topic/Product%20Specifications%20for%20SQL%20Server%202016.md)  
  
  