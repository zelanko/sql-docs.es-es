---
title: Requisitos de hardware y software para instalar SQL Server 2016 | Microsoft Docs
ms.custom: ''
ms.date: 11/06/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- Setup [SQL Server], software
- software [SQL Server]
- installing SQL Server, software
- operating systems [SQL Server], SQL Server requirements
- Setup [SQL Server], cross-language support
- operating systems [SQL Server], cross-language support
- network connections [SQL Server], requirements
- disk space [SQL Server], SQL Server installations
- WOW [SQL Server]
- Setup [SQL Server], hardware
- dependencies [SQL Server], SQL Server installations
- cluster hardware requirements [SQL Server]
- endpoints [SQL Server], SQL Server installations
- Internet [SQL Server], SQL Server installations
- hardware [SQL Server]
- Windows on Windows [SQL Server]
- installing SQL Server, hardware
- Setup Configuration Checker
- SCC [SQL Server]
- operating systems [SQL Server]
- space [SQL Server], SQL Server installations
- system configuration checker
- installing SQL Server, cross-language support
- Internet [SQL Server]
- space [SQL Server]
- extended system support [SQL Server]
- 64-bit edition [SQL Server]
- failover clustering [SQL Server]
- failover clustering [SQL Server], hardware requirements
- 32-bit edition [SQL Server]
- locales [SQL Server], SQL Server installations
- cross-language support
- disk space [SQL Server]
- localized SQL Server versions
ms.assetid: 09bcf20b-0a40-4131-907f-b61479d5e4d8
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 093a70a8e9651271aa2a8df4641f6f1e568fc2a7
ms.sourcegitcommit: c0b3b3d969af668d19b1bba04fa0c153cc8970fd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/11/2019
ms.locfileid: "57756740"
---
# <a name="hardware-and-software-requirements-for-installing-sql-server"></a>Requisitos de hardware y software para instalar SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se enumeran los requisitos mínimos de hardware y software para instalar y ejecutar [!INCLUDE[ssNoVer](../../includes/ssnoversion-md.md)] en el sistema operativo Windows. 

[!INCLUDE[sscurrent](../../includes/sssqlv14-md.md)] introduce compatibilidad con [!INCLUDE[ssNoVer](../../includes/ssnoversion-md.md)] en Linux. Para obtener más información, consulte [Requisitos de hardware y software para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en Linux](../../linux/sql-server-linux-setup.md#system). 

> Este artículo se aplica a [!INCLUDE[ss2016](../../includes/sssql15-md.md)] y versiones posteriores. 
  
**Pruébelo:**  
  
-   Descargue SQL Server desde el [**Centro de evaluación**.](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016) 
  
-   Ponga en marcha una máquina virtual con [**SQL Server 2016**](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm) ya instalado.  
  
**Las siguientes consideraciones son válidas para todas las ediciones:**  
  
-   Se recomienda ejecutar [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] en equipos con los formatos de archivo NTFS o ReFS. [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] se puede instalar en un equipo con el sistema de archivos FAT32, pero no se recomienda porque es menos seguro que el sistema de archivos NTFS o ReFS.  
  
-   El programa de instalación de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bloqueará las instalaciones en unidades de disco de solo lectura, asignadas o comprimidas.  
  
-   La instalación no se lleva a cabo si el programa de instalación se inicia a través de una Conexión a Escritorio remoto con los medios de un recurso local en el cliente RDC. Para realizar la instalación de forma remota, los medios deben estar en un recurso compartido de red o localmente en una máquina virtual o física. Los medios de instalación de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden estar en un recurso compartido de red, en una unidad asignada, en una unidad local o como una imagen ISO de una máquina virtual.  
  
-   Un requisito previo de la instalación de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] es tener .NET 4.6.1. El programa de instalación instalará automáticamente .NET 4.6.1 cuando se seleccione [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
-   El programa de instalación de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala los siguientes componentes de software que el producto necesita:  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client  
  
    -   Archivos auxiliares del programa de instalación de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]   
  
-   Para conocer los requisitos mínimos de versión para instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en [!INCLUDE[win8srv](../../includes/win8srv-md.md)] o [!INCLUDE[win8](../../includes/win8-md.md)], vea [Instalar SQL Server en Windows Server 2012 o Windows 8](https://support.microsoft.com/kb/2681562) (https://support.microsoft.com/kb/2681562).  
  
##  <a name="hwswr"></a> Requisitos de hardware y software  
Los siguientes requisitos se aplican a todas las instalaciones:  
  
|Componente|Requisito|  
|---------------|-----------------|  
|.NET Framework|[!INCLUDE[sql2016](../../includes/sssql15-md.md)] RC1 y las versiones posteriores necesitan [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.6 para el Motor de base de datos, Master Data Services o la replicación. El programa de instalación de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] instala automáticamente [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] también se puede instalar manualmente desde [Microsoft .NET Framework 4.6 (instalador web) para Windows](https://support.microsoft.com/kb/3045560).<br/><br/>[!INCLUDE[sql2019](../../includes/sssqlv15-md.md)] requiere .NET Framework 4.6.2. Está disponible en el [Centro de descarga](https://www.microsoft.com/download/details.aspx?id=53344).<br/><br/> Para ver más información, recomendaciones y directrices sobre [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.6, consulte la [Guía de implementación de .NET Framework para desarrolladores](https://msdn.microsoft.com/library/ee942965\(v=vs.110\).aspx).<br/><br/>[!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]y [!INCLUDE[winblue_server_2](../../includes/winblue-server-2-md.md)] necesitan [KB2919355](https://support.microsoft.com/kb/2919355) para instalar [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4.6.|  
|Software de red|Los sistemas operativos admitidos para [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] tienen software de red integrado. Las instancias con nombre y predeterminadas de una instalación independiente admiten los siguientes protocolos de red: Memoria compartida, canalizaciones con nombre, TCP/IP y VIA.<br/><br/> **Nota:** El protocolo VIA no es compatible con los clústeres de conmutación por error. Los clientes o las aplicaciones que se ejecutan en el mismo nodo del clúster de conmutación por error que la instancia de SQL Server pueden usar el protocolo de memoria compartida para conectarse a SQL Server con la dirección de la canalización local. Sin embargo, este tipo de conexión no es compatible con clúster y generará un error después de la conmutación por error de una instancia. Por tanto, no se recomienda y solo se debe usar en escenarios muy específicos.<br/><br/> **Importante:** El protocolo VIA está desusado. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]<br/><br/> Para obtener más información acerca de los protocolos de red y las bibliotecas de red, vea [Network Protocols and Network Libraries](../../sql-server/install/network-protocols-and-network-libraries.md).|  
|Disco duro|[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] requiere un mínimo de 6 GB de espacio disponible en disco.<br/><br/> Las necesidades de espacio en disco variarán según los componentes de [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] que instale. Para obtener más información, vea [Requisitos de espacio en disco duro](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#HardDiskSpace) en este artículo. Para obtener información acerca de los tipos de almacenamiento admitidos para los archivos de datos, vea [Storage Types for Data Files](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#StorageTypes)|  
|Unidad|Para la instalación desde disco se necesita una unidad de DVD.|  
|Monitor|[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] requiere Super VGA (800x600) o un monitor de una resolución mayor.|  
|Internet|La funcionalidad de Internet necesita acceso a Internet (no necesariamente de carácter gratuito).|  
  
> [!NOTE]
> La ejecución de [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] en una máquina virtual será más lenta que la ejecución nativa debido a la sobrecarga de virtualización.  
  
> [!IMPORTANT]
> Existen otros requisitos de hardware y software para la característica PolyBase. Para obtener más información, vea [Introducción a PolyBase](../../relational-databases/polybase/get-started-with-polybase.md).  
  
##  <a name="pmosr"></a> Requisitos de procesador, memoria y sistema operativo  
 Los siguientes requisitos de memoria y procesador se aplican a todas las ediciones de [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]:  
  
|Componente|Requisito|  
|---------------|-----------------|  
|Memoria \*|**Mínimo:**<br/><br/> Ediciones Express: 512 MB<br/><br/> Todas las demás ediciones: 1 GB<br/><br/> **Recomendado:**<br/><br/> Ediciones Express: 1 GB<br/><br/> Todas las demás ediciones: Al menos 4 GB y debe aumentar a medida que el tamaño de la base de datos aumente para asegurar un rendimiento óptimo.|  
|Velocidad del procesador|**Mínimo:** Procesador x64: 1,4 GHz<br/><br/> **Recomendado:** 2 GHz o superior|  
|Tipo de procesador|Procesador x64: AMD Opteron, AMD Athlon 64, Intel Xeon compatible con Intel EM64T, Intel Pentium IV compatible con EM64T|  
  
> [!NOTE]  
> La instalación de [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] es posible únicamente en procesadores x64. Ya no es viable en procesadores x86.  
  
 \* La memoria mínima necesaria para instalar el componente [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] en [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) es de 2 GB de RAM, que es independiente del requisito de memoria mínima de [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]. Para obtener información acerca de cómo instalar DQS, vea [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md).  
  
 **Compatibilidad con WOW64:**  
  
 WOW64 ((Windows de 32 bits sobre Windows de 64 bits) es una característica de las ediciones de 64 bits de Windows que permite que las aplicaciones de 32 bits se ejecuten de forma nativa en el modo de 32 bits. Las aplicaciones funcionan en el modo de 32 bits, aunque el sistema operativo subyacente sea de 64 bits. WOW64 no se admite en instalaciones de [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] . Sin embargo, las Herramientas de administración sí se admiten en WOW64.  
  
 **Compatibilidad con el sistema operativo:**  
  
 Las ediciones de [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] se clasifican en lo siguiente:  
  
-   [Ediciones principales](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#TOP_Principal)  
  
-   [Ediciones de amplio uso](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#TOP_Breadth)  
  
> [!NOTE]  
> Dos excepciones a la compatibilidad de sistema operativo indicada en esta sección son las siguientes características de Business Intelligence para [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] y versiones anteriores, que se pueden instalar en Windows Server 2008 R2 SP1 o posteriores:  
>  
>-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] - SharePoint  
> 
>-   Complemento[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para productos de SharePoint  

**Compatibilidad con Server Core:**

 ahora, [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] se admite en las instalaciones Server Core de Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 y Windows Server 2019. 

[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] se puede instalar en el modo Server Core en las siguientes ediciones de Windows Server:

|                              |                                |
| :------------------------    | :------------------------------|
| Windows Server 2019 Standard | Windows Server 2019 Datacenter |
| Windows Server 2016 Standard | Windows Server 2016 Datacenter |
| Windows Server 2012 R2 Standard | Windows Server 2012 R2 Datacenter|
| Windows Server 2012 Standard | Windows Server 2012 Datacenter |
| Windows Server 2008 R2 SP1 Standard | Windows Server 2008 R2 SP1 Datacenter |
| Windows Server 2008 R2 SP1 Enterprise | Windows Server 2008 R2 SP1 Web|
   | &nbsp; | &nbsp; |

Para más información sobre cómo instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] en Server Core, vea [Instalar SQL Server en Server Core](../../database-engine/install-windows/install-sql-server-on-server-core.md).  

  
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
  
###  <a name="TOP_Principal"></a> Principal Editions of [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]  
 La tabla siguiente se muestran los requisitos del sistema operativo para las ediciones principales de [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]:  
  
|Edición de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] |Sistema operativo compatible|  
|---------------------------------------|--------------------------------|  
|[!INCLUDE[ssEnterprise](../../includes/ssenterprise-md.md)]|[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2019_essentials_md](../../includes/winserver2019-essentials-md.md)] <br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_essentials_md](../../includes/winserver2016-essentials-md.md)] <br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation|  
|[!INCLUDE[ssStandard](../../includes/ssstandard-md.md)]|[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2019_essentials_md](../../includes/winserver2019-essentials-md.md)] <br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_essentials_md](../../includes/winserver2016-essentials-md.md)] <br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation<br/><br/> Windows 10 Home<br/><br/> Windows 10 Professional<br/><br/> Windows 10 Enterprise<br/><br/>Windows 10 IoT Enterprise<br/><br/>[!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]<br/><br/>[!INCLUDE[win8](../../includes/win8-md.md)]<br/><br/>[!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]<br/><br/>[!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]|  
|[!INCLUDE[ssWeb](../../includes/ssweb-md.md)]|[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2019_essentials_md](../../includes/winserver2019-essentials-md.md)] <br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_essentials_md](../../includes/winserver2016-essentials-md.md)] <br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation|  

  
###  <a name="TOP_Breadth"></a> Ediciones de amplio uso de [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]  
 La tabla siguiente se muestran los requisitos del sistema operativo para las ediciones de amplio uso de [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]:  
  
|Edición de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] |Sistema operativo compatible|  
|---------------------------------------|--------------------------------|  
|[!INCLUDE[ssDeveloper](../../includes/ssdeveloper-md.md)]|[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2019_essentials_md](../../includes/winserver2019-essentials-md.md)] <br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_essentials_md](../../includes/winserver2016-essentials-md.md)] <br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation<br/><br/> Windows 10 Home<br/><br/> Windows 10 Professional<br/><br/> Windows 10 Enterprise<br/><br/>Windows 10 IoT Enterprise<br/><br/>[!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]<br/><br/>[!INCLUDE[win8](../../includes/win8-md.md)]<br/><br/>[!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]<br/><br/>[!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]|  
|[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]|[!INCLUDE[winserver2019_datacenter_md](../../includes/winserver2019-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2019_standard_md](../../includes/winserver2019-standard-md.md)]<br/><br/>[!INCLUDE[winserver2019_essentials_md](../../includes/winserver2019-essentials-md.md)] <br/><br/>[!INCLUDE[winserver2016_datacenter_md](../../includes/winserver2016-datacenter-md.md)]<br/><br/>[!INCLUDE[winserver2016_standard_md](../../includes/winserver2016-standard-md.md)]<br/><br/>[!INCLUDE[winserver2016_essentials_md](../../includes/winserver2016-essentials-md.md)] <br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] R2 Foundation<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Datacenter<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Standard<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Essentials<br/><br/>[!INCLUDE[win8srv](../../includes/win8srv-md.md)] Foundation<br/><br/> Windows 10 Home<br/><br/> Windows 10 Professional<br/><br/> Windows 10 Enterprise<br/><br/>Windows 10 IoT Enterprise<br/><br/>[!INCLUDE[winblue_client_2](../../includes/winblue-client-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_pro_2](../../includes/winblue-client-pro-2-md.md)]<br/><br/>[!INCLUDE[winblue_client_ent_2](../../includes/winblue-client-ent-2-md.md)]<br/><br/>[!INCLUDE[win8](../../includes/win8-md.md)]<br/><br/>[!INCLUDE[win8_client_pro_2](../../includes/win8-client-pro-2-md.md)]<br/><br/>[!INCLUDE[win8_client_ent_2](../../includes/win8-client-ent-2-md.md)]|  

  
##  <a name="CrossLanguageSupport"></a> Compatibilidad entre idiomas  
 Para más información sobre la compatibilidad entre idiomas y consideraciones sobre la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en idiomas localizados, consulte [Versiones en idioma local en SQL Server](../../sql-server/install/local-language-versions-in-sql-server.md).  
  
##  <a name="HardDiskSpace"></a> Requisitos de espacio en disco duro  
 Durante la instalación de [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)], Windows Installer crea archivos temporales en la unidad del sistema. Antes de ejecutar el programa de instalación para instalar o actualizar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], compruebe que dispone de al menos 6,0 GB de espacio en disco en la unidad del sistema para estos archivos. Este requisito es aplicable incluso si instala todos los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en una unidad distinta de la predeterminada.  
  
 Los requisitos reales de disco duro dependen de la configuración del sistema y de las características que decida instalar. En la tabla siguiente se muestran los requisitos de espacio en disco de los componentes de [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] :  
  
|**Característica**|**Requisito de espacio en disco**|  
|-----------------|--------------------------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] y archivos de datos, replicación, búsqueda de texto completo y Data Quality Services|1480 MB|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] (como arriba) con R Services (In-Database)|2744 MB|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] (como arriba) con Servicio de consultas de PolyBase para datos externos|4194 MB|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y archivos de datos|698 MB|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|967 MB|  
|[!INCLUDE[rsql_platform](../../includes/rsql-platform-md.md)] (independiente)|280 MB|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] - SharePoint|1203 MB|  
|Complemento[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Add-in for SharePoint Products|325 MB|  
|[!INCLUDE[ssDQSClient](../../includes/ssdqsclient-md.md)]|121 MB|  
|Conectividad con las herramientas de cliente|328 MB|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|306 MB|  
|Componentes de cliente (excepto los componentes de los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y las herramientas de Integration Services)|445 MB|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|280 MB|  
|Componentes de Libros en pantalla de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ver y administrar el contenido de la Ayuda*|27 MB|  
|Todas las características|8030 MB|  
  
 *Los requisitos de espacio en disco para el contenido descargado de los Libros en pantalla son 200 MB.  
  
##  <a name="StorageTypes"></a> Tipos de almacenamiento para los archivos de datos  
 Los tipos admitidos de almacenamiento para los archivos de datos son:  
  
-   Disco local  
    > [!WARNING]  
    > La instalación de clústeres de conmutación por error de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite el disco local solo para instalar los archivos tempdb. Asegúrese de que la ruta de acceso especificada para los archivos de datos y registro de tempdb es válida en todos los nodos del clúster. Durante la conmutación por error, si los directorios de tempdb no están disponibles en el nodo de destino de la conmutación por error, el recurso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no podrá ponerse en línea.

    > [!IMPORTANT]
    > En la actualidad, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite unidades de disco con tamaños de sector nativo estándar de 512 bytes y 4 KB.  En los discos duros con tamaños de sector mayores de 4 KB se pueden producir errores al intentar almacenar archivos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en ellos.  Vea [Hard disk drive sector-size support boundaries in SQL Server](https://support.microsoft.com/kb/926930) (Límites de compatibilidad de tamaños de sector de unidades de disco duro en SQL Server) para obtener más información sobre la compatibilidad de tamaños de sector de disco duro en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
-   Almacenamiento compartido  

-   [Espacios de almacenamiento directo \(S2D\)](https://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)
  
-   Recurso compartido de archivos SMB  
  
    > [!NOTE]  
    > El almacenamiento SMB no se admite para los archivos de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en instalaciones independientes o en clúster. En su lugar, use almacenamiento de conexión directa, una red de área de almacenamiento o S2D.  
  
    > [!IMPORTANT]  
    > El almacenamiento SMB podría estar hospedado en un servidor de archivos Windows o en un dispositivo de almacenamiento SMB de terceros. Si se utiliza un servidor de archivos Windows, la versión de Windows File Server debería ser 2008 o posterior. Para obtener más información sobre la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante un recurso compartido de archivos SMB como opción de almacenamiento, vea [Instalar SQL Server con el recurso compartido de archivos SMB como opción de almacenamiento](../../database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option.md).  
  
  
  
##  <a name="DC_support"></a> Instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un controlador de dominio  
 Por razones de seguridad, se recomienda que no se instale [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] en un controlador de dominio. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no bloqueará la instalación en un equipo que sea un controlador de dominio, pero se aplican las limitaciones siguientes:  
  
-   No puede ejecutar los servicios [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un controlador de dominio bajo una cuenta del servicio local.  
  
-   Una vez instalado en un equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , no puede cambiar el equipo de un miembro de dominio a un controlador de dominio. Debe desinstalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de cambiar el equipo host a un controlador de dominio.  
  
-   Una vez instalado en un equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , no puede cambiar el equipo de un controlador de dominio a un miembro de dominio. Debe desinstalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de cambiar el equipo host a un miembro de dominio.  
  
-   Las instancias del clúster de conmutación por error de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se admiten si los nodos de clúster son controladores de dominio.  
  
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se admite en un controlador de dominio de solo lectura. El programa de instalación de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede crear grupos de seguridad ni suministrar cuentas de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un controlador de dominio de solo lectura. En este escenario, se producirá un error de instalación.  

- Una instancia de clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se admite en un entorno donde solo se puede acceder a un controlador de dominio de solo lectura. 
  
## <a name="see-also"></a>Consulte también  
 [Planear una instalación de SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Consideraciones de seguridad para una instalación de SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)   
 [Especificaciones de producto de SQL Server 2016](https://msdn.microsoft.com/library/6445fd53-6844-4170-a86b-7fe76a9f64cb)  
  
  
