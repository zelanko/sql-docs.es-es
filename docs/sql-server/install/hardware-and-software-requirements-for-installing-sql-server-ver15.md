---
title: Requisitos de hardware y software para la instalación de SQL Server | Microsoft Docs
ms.custom: sqlfreshmay19
ms.date: 11/04/2019
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
ms.openlocfilehash: 88ed55a3c2890864e3e9623f3fa53ca3e747350c
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/04/2019
ms.locfileid: "73536181"
---
# <a name="hardware-and-software-requirements-for-installing-sql-server"></a>Requisitos de hardware y software para la instalación de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se enumeran los requisitos mínimos de hardware y software para instalar y ejecutar [!INCLUDE[ssNoVer](../../includes/ssnoversion-md.md)] en el sistema operativo Windows.

[!INCLUDE[sscurrent](../../includes/sssqlv14-md.md)] ha introducido compatibilidad con [!INCLUDE[ssNoVer](../../includes/ssnoversion-md.md)] en Linux. Para obtener más información, consulte [Requisitos de hardware y software para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en Linux](../../linux/sql-server-linux-setup.md#system). 

**Pruébelo:**  
  
- Descargue SQL Server desde el [**Centro de evaluación**.](https://www.microsoft.com/evalcenter/evaluate-sql-server-2019-rc) 
  
<!-- 
- Spin up a Virtual Machine with [**SQL Server 2017**](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm) already installed.  
-->
  
**Las siguientes consideraciones son válidas para todas las ediciones:**  
  
- El programa de instalación de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bloqueará las instalaciones en unidades de disco de solo lectura, asignadas o comprimidas.  
  
- La instalación no se lleva a cabo si el programa de instalación se inicia a través de una Conexión a Escritorio remoto con los medios de un recurso local en el cliente RDC. Para realizar la instalación de forma remota, los medios deben estar en un recurso compartido de red o localmente en una máquina virtual o física. Los medios de instalación de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden estar en un recurso compartido de red, en una unidad asignada, en una unidad local o como una imagen ISO de una máquina virtual.
- El programa de instalación de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala los siguientes componentes de software que el producto necesita:  
  
    - [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client  
  
    - Archivos auxiliares del programa de instalación de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  

##  <a name="hwswr"></a> Requisitos de hardware y software  
Los siguientes requisitos se aplican a todas las instalaciones:  
  
|Componente|Requisito|  
|---------------|-----------------|  
|Sistema operativo|Windows 10 TH1 1507 o una versión superior<br/><br>Windows Server 2016 o una versión posterior<br/><br/>
|.NET Framework|Los sistemas operativos mínimos incluyen, como mínimo, .NET Framework.|  
|Software de red|Los sistemas operativos admitidos para [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] tienen software de red integrado. Las instancias con nombre y predeterminadas de una instalación independiente admiten los siguientes protocolos de red: Memoria compartida, canalizaciones con nombre y TCP/IP.<br/><br/> |  
|Disco duro|[!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] requiere un mínimo de 6 GB de espacio disponible en disco.<br/><br/> Las necesidades de espacio en disco variarán según los componentes de [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] que instale. Para obtener más información, vea [Requisitos de espacio en disco duro](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#HardDiskSpace) en este artículo. Para obtener información acerca de los tipos de almacenamiento admitidos para los archivos de datos, vea [Tipos de almacenamiento para los archivos de datos](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#StorageTypes)|  
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
|Memoria \*|**Mínimo:**<br/><br/> Ediciones Express: 512 MB<br/><br/> Las demás ediciones: 1 GB<br/><br/> **Recomendado:**<br/><br/> Ediciones Express: 1 GB<br/><br/> Las demás ediciones: Al menos 4 GB, que debe aumentar a medida que el tamaño de la base de datos aumente para asegurar un rendimiento óptimo.|  
|Velocidad del procesador|**Mínimo:** Procesador x64: 1,4 GHz<br/><br/> **Recomendado:** 2.0 GHz o superior|  
|Tipo de procesador|Procesador x64: AMD Opteron, AMD Athlon 64, Intel Xeon compatible con Intel EM64T, Intel Pentium IV compatible con EM64T|  
  
> [!NOTE]  
> La instalación de [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] es posible únicamente en procesadores x64. Ya no es viable en procesadores x86.  
  
 \* La memoria mínima necesaria para instalar el componente [!INCLUDE[ssDQSServer](../../includes/ssdqsserver-md.md)] en [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] (DQS) es de 2 GB de RAM, que es independiente del requisito de memoria mínima de [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)]. Para obtener información acerca de cómo instalar DQS, vea [Install Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md).  

**Compatibilidad con Server Core:**

La instalación de SQL Server 2019 en el modo Server Core es compatible con las siguientes ediciones de Windows Server:

|                              |
| :------------------------  |
| Windows Server 2019 Core | 
| Windows Server 2016 Core |
| &nbsp; | 

Para obtener más información sobre cómo instalar SQL Server en Server Core, vea [Instalar SQL Server en Server Core](../../database-engine/install-windows/install-sql-server-on-server-core.md).  

###  <a name="TOP_Principal"></a> Compatibilidad del sistema operativo   

La siguiente tabla muestra qué ediciones de SQL Server 2019 son compatibles con las versiones de Windows:  
  

| Edición de SQL Server:               | Enterprise | Desarrollador | Estándar | Web | Express |  
| :------------------------       | :--------- | :-------- | :------- | :-- | :------ | 
| Windows Server 2019 Datacenter    |    Sí     |    Sí    |    Sí   | Sí |   Sí   |
| Windows Server 2019 Standard      |    Sí     |    Sí    |    Sí   | Sí |   Sí   |
| Windows Server 2019 Essentials    |    Sí     |    Sí    |    Sí   | Sí |   Sí   |
| Windows Server 2016 Datacenter    |    Sí     |    Sí    |    Sí   | Sí |   Sí   |
| Windows Server 2016 Standard      |    Sí     |    Sí    |    Sí   | Sí |   Sí   |
| Windows Server 2016 Essentials    |    Sí     |    Sí    |    Sí   | Sí |   Sí   |
| &nbsp; | &nbsp; |


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
  
- Disco local 
    - En la actualidad, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite unidades de disco con tamaños de sector nativo estándar de 512 bytes y 4 KB.  En los discos duros con tamaños de sector mayores de 4 KB se pueden producir errores al intentar almacenar archivos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en ellos.  Vea [Hard disk drive sector-size support boundaries in SQL Server](https://support.microsoft.com/kb/926930) (Límites de compatibilidad de tamaños de sector de unidades de disco duro en SQL Server) para obtener más información sobre la compatibilidad de tamaños de sector de disco duro en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 
    - La instalación de clústeres de conmutación por error de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite el disco local solo para instalar los archivos tempdb. Asegúrese de que la ruta de acceso especificada para los archivos de datos y registro de tempdb es válida en todos los nodos del clúster. Durante la conmutación por error, si los directorios de tempdb no están disponibles en el nodo de destino de la conmutación por error, el recurso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no podrá ponerse en línea.
- Almacenamiento compartido  
- [Espacios de almacenamiento directo \(S2D\)](https://technet.microsoft.com/windows-server-docs/storage/storage-spaces/storage-spaces-direct-overview)  
- Recurso compartido de archivos SMB  
    - El almacenamiento SMB no se admite para los archivos de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en instalaciones independientes o en clúster. En su lugar, use almacenamiento de conexión directa, una red de área de almacenamiento o S2D. 
    - El almacenamiento SMB podría estar hospedado en un servidor de archivos Windows o en un dispositivo de almacenamiento SMB de terceros. Si se utiliza un servidor de archivos Windows, la versión de Windows File Server debería ser 2008 o posterior. Para obtener más información sobre la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante un recurso compartido de archivos SMB como opción de almacenamiento, vea [Instalar SQL Server con el recurso compartido de archivos SMB como opción de almacenamiento](../../database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option.md).  
  
  
  
##  <a name="DC_support"></a> Instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un controlador de dominio  
 Por razones de seguridad, se recomienda que no se instale [!INCLUDE[ssCurrent](../../includes/ssnoversion-md.md)] en un controlador de dominio. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no bloqueará la instalación en un equipo que sea un controlador de dominio, pero se aplican las limitaciones siguientes:  
  
- No puede ejecutar los servicios [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un controlador de dominio bajo una cuenta del servicio local.    
- Una vez instalado en un equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , no puede cambiar el equipo de un miembro de dominio a un controlador de dominio. Debe desinstalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de cambiar el equipo host a un controlador de dominio.    
- Una vez instalado en un equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , no puede cambiar el equipo de un controlador de dominio a un miembro de dominio. Debe desinstalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de cambiar el equipo host a un miembro de dominio.   
- Las instancias del clúster de conmutación por error de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se admiten si los nodos de clúster son controladores de dominio.   
- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se admite en un controlador de dominio de solo lectura. El programa de instalación de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede crear grupos de seguridad ni suministrar cuentas de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un controlador de dominio de solo lectura. En este escenario, se producirá un error de instalación. 
- Una instancia de clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se admite en un entorno donde solo se puede acceder a un controlador de dominio de solo lectura. 
  
## <a name="see-also"></a>Vea también  
 [Planear una instalación de SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Consideraciones de seguridad para una instalación de SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)   

