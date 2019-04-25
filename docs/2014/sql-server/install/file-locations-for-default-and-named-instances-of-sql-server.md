---
title: Ubicaciones de archivos para las instancias predeterminadas y con nombre de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 463c570e-9f75-4653-b3b8-4d61753b0013
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ca9df655e00b1f2fd1919f30bb1bb166e2556b91
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62505122"
---
# <a name="file-locations-for-default-and-named-instances-of-sql-server"></a>Ubicaciones de archivos para las instancias predeterminadas y con nombre de SQL Server
  Una instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se compone de una o más instancias independientes. Una instancia, ya sea predeterminada o con nombre, tiene su propio conjunto de archivos de programa y de datos, así como un conjunto de archivos comunes compartidos entre todas las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] del equipo.  
  
 En una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que incluya el [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], cada componente tiene un conjunto completo de datos y de archivos ejecutables, así como de archivos comunes compartidos por todos los componentes.  
  
 Para aislar las ubicaciones de instalación de cada componente, se generan identificadores de instancia únicos para cada componente de una determinada instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Los archivos de programa y los archivos de datos no se pueden instalar en una unidad de disco extraíble, en un sistema de archivos que use compresión, en un directorio en el que haya ubicados archivos del sistema ni en unidades compartidas en una instancia en clúster de conmutación por error.  
>   
>  Las bases de datos del sistema (maestra, modelo, MSDB y tempdb) y las bases de datos de usuario del [!INCLUDE[ssDE](../../includes/ssde-md.md)] se pueden instalar con el servidor de archivos del Bloque de mensajes del servidor (SMB) como opción de almacenamiento. Esto se aplica tanto a las instalaciones independientes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como a las instalaciones de clústeres de conmutación por error (FCI) de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para más información, consulte [Instalar SQL Server con el recurso compartido de archivos SMB como opción de almacenamiento](../../database-engine/install-windows/install-sql-server-with-smb-fileshare-as-a-storage-option.md).  
>   
>  No elimine ninguno de los directorios siguientes ni su contenido: Binn, Data, Ftdata, HTML o 1033. Si fuera necesario, puede eliminar otros directorios; no obstante, es posible que no pueda recuperar algunas de las funciones o datos perdidos sin tener que desinstalar y volver a instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No elimine ni modifique ninguno de los archivos .htm del directorio HTML. Son necesarios para que las herramientas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] funcionen correctamente.  
  
## <a name="shared-files-for-all-instances-of-includessnoversionincludesssnoversion-mdmd"></a>Archivos compartidos para todas las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Los archivos comunes que usan todas las instancias en un único equipo se instalan en la carpeta [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)], donde \<*unidad*> es la letra de la unidad en la que están instalados los componentes. La unidad predeterminada es normalmente la C.  
  
## <a name="file-locations-and-registry-mapping"></a>Ubicaciones de archivos y asignaciones del Registro  
 Durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , se genera un identificador de instancia en cada componente de servidor. Los componentes de servidor de esta versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] son el [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 El identificador de instancia predeterminado se construye con el formato siguiente:  
  
-   MSSQL para el [!INCLUDE[ssDE](../../includes/ssde-md.md)], seguido del número de versión principal, un guión bajo y la versión secundaria cuando proceda, un punto y, a continuación, el nombre de instancia.  
  
-   MSAS para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], seguido del número de versión principal, un guión bajo y la versión secundaria cuando proceda, un punto y, a continuación, el nombre de instancia.  
  
-   MSRS para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], seguido del número de versión principal, un guión bajo y la versión secundaria cuando proceda, un punto y, a continuación, el nombre de instancia.  
  
 A continuación se enumeran algunos ejemplos de identificadores de instancia predeterminados de esta versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   MSSQL12.MSSQLSERVER para una instancia predeterminada de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
-   MSAS12.MSSQLSERVER para una instancia predeterminada de [!INCLUDE[ssASCurrent](../../includes/ssascurrent-md.md)].  
  
-   MSSQL12.MyInstance para una instancia con nombre de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] denominada "MyInstance".  
  
 La estructura de directorios para una instancia con nombre de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] que incluyera el [!INCLUDE[ssDE](../../includes/ssde-md.md)] y [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], se denominara "MyInstance" y estuviera instalada en los directorios predeterminados sería como sigue:  
  
-   C:\Archivos de programa\Microsoft SQL Server\MSSQL12.MyInstance\  
  
-   C:\Archivos de programa\Microsoft SQL Server\MSAS12.MyInstance\  
  
 Puede especificar cualquier valor para el identificador de instancia, pero evite los caracteres especiales y las palabras clave reservadas.  
  
 Puede especificar un identificador de instancia no predeterminado durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . En lugar de \<Archivos de programa>\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], se usa una \<ruta de acceso personalizada>\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si el usuario decide cambiar el directorio de instalación predeterminado. Tenga en cuenta que no se admiten identificadores de instancia que comienzan por un subrayado (_) o que contienen el signo de almohadilla (#) o el signo de dólar ($).  
  
> [!NOTE]  
>  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y los componentes de cliente no reconocen las instancias y, por consiguiente, no tienen asignado un identificador de instancia. De forma predeterminada, los componentes que no reconocen las instancias se instalan en un único directorio: [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]. Si cambia la ruta de instalación de un componente compartido, cambiará también la de los demás componentes compartidos. Las instalaciones posteriores instalan componentes que no reconocen instancias en el mismo directorio que la instalación original.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] es el único componente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que permite cambiar el nombre de las instancias después de la instalación. Si se cambia el nombre una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , el identificador de la instancia no cambiará. Después de completarse el cambio de nombre de la instancia, los directorios y claves del Registro continuarán utilizando el identificador de instancia creado durante la instalación.  
  
 El subárbol del Registro se crea en HKLM\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<*Instance_ID*> para los componentes dependientes de la instancia. Por ejemplo,  
  
-   HKLM\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12.MyInstance  
  
-   HKLM\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSAS12.MyInstance  
  
-   HKLM\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSRS12.MyInstance  
  
 El Registro también mantiene una asignación de identificador de instancia a nombre de instancia. La asignación de identificador de instancia a nombre de instancia se mantiene de la siguiente forma:  
  
-   [HKEY_LOCAL_MACHINE\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\Instance Names\SQL] "InstanceName"="MSSQL12"  
  
-   [HKEY_LOCAL_MACHINE\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\Instance Names\OLAP] "InstanceName"="MSAS12"  
  
-   [HKEY_LOCAL_MACHINE\Software\\[!INCLUDE[msCoName](../../includes/msconame-md.md)]\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\Instance Names\RS] "InstanceName"="MSRS12"  
  
## <a name="specifying-file-paths"></a>Especificar rutas de acceso a los archivos  
 Durante la instalación, puede cambiar la ruta de instalación de las siguientes características:  
  
 La ruta de instalación solo aparece para las características cuya carpeta de destino puede configurar el usuario:  
  
|Componente|Ruta de acceso predeterminada<sup>1, 2</sup>|Puede configurar<sup>3</sup> o se ha corregido la ruta de acceso|  
|---------------|---------------------------------|--------------------------------------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] componentes de servidor|Archivos \Program\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12.\< InstanceID >\|Configurable|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] archivos de datos|Archivos \Program\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12.\< InstanceID >\|Configurable|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] servidores|Archivos \Program\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSAS12.\< InstanceID >\|Configurable|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] archivos de datos|Archivos \Program\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSAS12.\< InstanceID >\|Configurable|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] servidor de informes|Archivos \Program\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSRS12.\< InstanceID > \Reporting\|Configurable|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] administrador de informes|Archivos \Program\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSRS12.\< InstanceID > \Reporting Services\ReportManager\|ruta de acceso fija|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|\<Directorio de instalación > \120\DTS\|Configurable<sup>4</sup>|  
|Componentes cliente (excepto bcp.exe y sqlcmd.exe)|\<Directorio de instalación > \120\Tools\|Configurable<sup>4</sup>|  
|Componentes cliente (bcp.exe y sqlcmd.exe)|\<Directorio de instalación>\Client SDK\ODBC\110\Tools\Binn|Ruta de acceso fija|  
|Objetos COM del servidor y la replicación|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]COM\\<sup>5</sup>|Ruta de acceso fija|  
|DLL de componentes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] del motor en tiempo de ejecución de transformación de datos, el motor de canalización de transformación de datos y la utilidad de símbolo del sistema `dtexec`|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\Binn|Ruta de acceso fija|  
|DLL que proporcionan compatibilidad con la conexión administrada para [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\Connections|Ruta de acceso fija|  
|DLL para cada tipo de enumeración que admita [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]DTS\ForEachEnumerators|Ruta de acceso fija|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , proveedores WMI|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Compartido\|ruta de acceso fija|  
|Componentes que se comparten entre todas las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]Compartido\|ruta de acceso fija|  
  
 <sup>1</sup>Asegúrese de que el \Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\ carpeta está protegida con permisos limitados.  
  
 <sup>2</sup>es la unidad predeterminada para estas ubicaciones *systemdrive*, normalmente la unidad C.  
  
 <sup>3</sup>rutas de acceso de instalación para las características secundarias están determinados por la ruta de instalación de la característica primaria.  
  
 <sup>4</sup>una sola ruta de instalación se comparte entre [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y componentes de cliente. Si cambia la ruta de instalación de un componente, cambiará también la de los otros componentes. Las instalaciones posteriores instalan los componentes en la misma ubicación que la instalación original.  
  
 <sup>5</sup>este directorio es utilizado por todas las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un equipo. Si aplica una actualización a alguna de las instancias del equipo, los cambios en los archivos de esta carpeta afectarán a todas las instancias en el equipo. Cuando agregue características a una instalación existente, no podrá cambiar la ubicación de una característica instalada anteriormente, ni especificar dicha ubicación para una característica nueva. Debe instalar características adicionales en los directorios ya establecidos por el programa de instalación, o desinstalar y volver a instalar el producto.  
  
> [!NOTE]  
>  En configuraciones en clúster, deberá seleccionar una unidad local que esté disponible en cada nodo del clúster.  
  
 Cuando especifique una ruta de instalación durante la instalación de los componentes de servidor o de los archivos de datos, el programa de instalación utilizará el identificador de instancia además de la ubicación especificada para el programa y los archivos de datos. El programa de instalación no utiliza el identificador de instancia para las herramientas y otros archivos compartidos. Tampoco utiliza ningún identificador de instancia para el programa y los archivos de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , aunque lo use para el depósito de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Si establece una ruta de instalación para la característica [!INCLUDE[ssDE](../../includes/ssde-md.md)] , el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizará dicha ruta como directorio raíz de todas las carpetas específicas de la instancia en dicha instalación, incluido SQL Data Files. En este caso, si establece la raíz en "C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12.\< InstanceName > \MSSQL\\", los directorios específicos de la instancia se agregarán al final de dicha ruta de acceso.  
  
 Los clientes que decidan usar la funcionalidad de actualización de USESYSDB en el Asistente para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (modo de UI del programa de instalación) pueden llegar con facilidad a una situación en la que el producto se instale en una estructura de carpetas recursiva. Por ejemplo, \< *SQLProgramFiles*> \MSSQL12\MSSQL\MSSQL10_50\MSSQL\Data\\. En su lugar, para usar la característica USESYSDB, establezca una ruta de instalación para la característica de archivos de datos de SQL (SQL Data Files) y no para la característica [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
> [!NOTE]
>  Los archivos de datos deberían encontrarse en un directorio secundario denominado Data. Por ejemplo, especificar C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12.\< NombreDeInstancia > \ para especificar la ruta de acceso raíz al directorio de datos de las bases de datos del sistema durante la actualización si los archivos de datos se encuentran en C:\Program Files\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12.\< NombreDeInstancia > \MSSQL\Data.  
  
## <a name="see-also"></a>Vea también  
 [Configuración del motor de base de datos - Directorios de datos](../../../2014/sql-server/install/database-engine-configuration-data-directories.md)   
 [Configuración de Analysis Services - Directorios de datos](../../../2014/sql-server/install/analysis-services-configuration-data-directories.md)  
  
  
