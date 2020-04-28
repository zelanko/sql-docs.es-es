---
title: Instale SQL Server 2014 en Server Core | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 1dd294cc-5b69-4d0c-9005-3e307b75678b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e3e244b2c4892d725e8e3ddf684b55a224138a50
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "73637674"
---
# <a name="install-sql-server-2014-on-server-core"></a>Instalar SQL Server 2014 en Server Core
  Puede instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en una instalación Server Core de [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 o de [!INCLUDE[win8srv](../../includes/win8srv-md.md)]. En este tema se proporcionan detalles específicos de la instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] en Server Core.  
  
 La opción de instalación Server Core para el sistema operativo [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] o [!INCLUDE[win8srv](../../includes/win8srv-md.md)] proporciona un entorno mínimo para ejecutar determinados roles de servidor. Esto ayuda a reducir los requisitos de administración y mantenimiento y la superficie de ataque para esos roles de servidor. Para obtener más información sobre Server Core tal y [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]como se implementa en, vea [Server Core para Windows Server 2008 R2](https://go.microsoft.com/fwlink/?LinkId=202439) (https://go.microsoft.com/fwlink/?LinkId=202439). Para obtener más información sobre Server Core tal y [!INCLUDE[win8srv](../../includes/win8srv-md.md)]como se implementa en, vea [Server Core para Windows Server 2012](https://msdn.microsoft.com/library/hh846323\(VS.85\).aspx) (https://msdn.microsoft.com/library/hh846323(VS.85).aspx).  
  
## <a name="prerequisites"></a>Prerequisites  
  
|Requisito|Cómo instalar|  
|-----------------|--------------------|  
|[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 2.0 SP2|Incluido en la instalación Server Core de [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 y [!INCLUDE[win8srv](../../includes/win8srv-md.md)]. Si no está habilitado, el programa de instalación lo habilita de forma predeterminada.<br /><br /> No es posible ejecutar las versiones 2.0, 3.0 y 3.5 en paralelo en un equipo. Cuando instala .NET Framework 3.5 SP1, obtiene los niveles 2.0 y 3.0 automáticamente.|  
|[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 3.5 SP1 Full Profile|Incluido en la instalación Server Core de [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1. Si no está habilitado, el programa de instalación lo habilita de forma predeterminada.<br /><br /> En un equipo con el sistema operativo de servidor Windows, debe descargar e instalar .NET Framework 3.5 SP1 antes de ejecutar el programa de instalación para instalar componentes dependientes de .NET 3.5 SP1.<br /><br /> Para obtener más información acerca de las recomendaciones e instrucciones sobre cómo adquirir y habilitar .NET Framework 3,5 [!INCLUDE[win8srv](../../includes/win8srv-md.md)]en, vea [consideraciones sobre la implementación de Microsoft .NET Framework 3,5](https://msdn.microsoft.com/library/windows/hardware/hh975396) (https://msdn.microsoft.com/library/windows/hardware/hh975396).|  
|[!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4 Server Core Profile|Para todas las ediciones de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] excepto [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], el programa de instalación instala [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4 Server Core Profile como un requisito previo.<br /><br /> Para [!INCLUDE[ssExpressEd11](../../includes/ssexpressed11-md.md)], descargue [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] 4 Server Core Profile desde [Microsoft .NET Framework 4 (instalador independiente) para Server Core](https://www.microsoft.com/download/details.aspx?id=17718) (https://www.microsoft.com/download/details.aspx?id=17718)y instálelo antes de continuar con la instalación.|  
|Windows Installer 4.5|Incluido con la instalación Server Core de [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 y [!INCLUDE[win8srv](../../includes/win8srv-md.md)].|  
|Windows PowerShell 2.0|Incluido con la instalación Server Core de [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 y [!INCLUDE[win8srv](../../includes/win8srv-md.md)].|  
  
##  <a name="supported-features"></a><a name="BK_SupportedFeatures"></a> Características admitidas  
 Use la tabla siguiente para encontrar qué características se admiten en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] en una instalación Server Core de [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 y [!INCLUDE[win8srv](../../includes/win8srv-md.md)].  
  
|Característica|Compatible|  
|-------------|---------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)] Servicios|Sí|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Replicación|Sí|  
|Búsqueda de texto completo|Sí|  
|[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|Sí|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|No|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Data Tools (SSDT)|No|  
|Conectividad con las herramientas de cliente|Sí|  
|Integration Services Server<sup>[1]</sup>|Sí|  
|Compatibilidad con las versiones anteriores de las herramientas de cliente|No|  
|SDK de las herramientas de cliente|No|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Libros en pantalla|No|  
|Herramientas de administración: básicas|Solo remoto<sup>[2]</sup>|  
|Herramientas de administración - Completa|Solo remoto<sup>[2]</sup>|  
|Distributed Replay Controller|No|  
|Distributed Replay Client|Solo remoto<sup>[2]</sup>|  
|SDK de conectividad de cliente SQL|Sí|  
|Microsoft Synchronization Framework|Sí<sup>[3]</sup>|  
|[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]|No|  
|[!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]|No|  
  
 <sup>[1]</sup> Para obtener más información sobre el nuevo servidor de Integration Services y sus [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]características en, consulte [Integration Services &#40;SSIS&#41; Server](../../integration-services/catalog/integration-services-ssis-server-and-catalog.md).  
  
 <sup>[2]</sup> No se admite la instalación de estas características en Server Core. Estos componentes se pueden instalar en un servidor diferente que no sea [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 o [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core y conectarse a los servicios de [!INCLUDE[ssDE](../../includes/ssde-md.md)] instalados en Server Core.  
  
 <sup>[3]</sup> Microsoft Sync Framework no se incluye en el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] paquete de instalación. Puede descargar la versión adecuada de Sync Framework desde este [centro de descarga](https://go.microsoft.com/fwlink/?LinkId=221788) de Microsofthttps://go.microsoft.com/fwlink/?LinkId=221788) (página e instalarla en un equipo que ejecute la instalación Server Core [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] de SP1 [!INCLUDE[win8srv](../../includes/win8srv-md.md)]o.  
  
## <a name="supported-scenario-matrix"></a>Matriz de escenarios admitidos  
 En la siguiente tabla se muestra la matriz de escenarios admitidos para instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] en una instalación Server Core de [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 y [!INCLUDE[win8srv](../../includes/win8srv-md.md)].  
  
|||  
|-|-|  
|Ediciones de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Todas [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] las ediciones de 64 bits<sup>[1]</sup>|  
|Idioma de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|Todos los idiomas|  
|Idioma de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el idioma o configuración regional (combinación) del sistema operativo|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en inglés en Windows en japonés<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en inglés en Windows en alemán<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en inglés en Windows en chino<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en inglés en Windows en árabe<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en inglés en Windows en tailandés<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en inglés en Windows en turco<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en inglés en Windows en portugués de Portugal<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en inglés en Windows en inglés|  
|Edición de Windows|[!INCLUDE[win8srv](../../includes/win8srv-md.md)] de 64 bits x64 Datacenter<br /><br /> [!INCLUDE[win8srv](../../includes/win8srv-md.md)] de 64 bits x64 Standard<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] S12 de 64 bits x64 Data Center Server Core<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 64 de bits x64 Enterprise Server Core<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 de 64 bits x64 Standard Server Core<br /><br /> [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 de 64 bits x64 Web Server Core|  
  
 <sup>[1]</sup> No se admite la instalación de la [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] versión de 32 bits de las ediciones en Server Core.  
  
## <a name="upgrading"></a>Actualizando  
 En las instalaciones básicas Server Core, se admite la actualización de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] .  
  
## <a name="installation"></a>Instalación  
 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no admite la instalación con el asistente de instalación en el sistema operativo Server Core. Al realizar la instalación en Server Core, el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite el modo totalmente silencioso mediante el uso del parámetro /Q o el modo silencioso simple mediante el parámetro /QS. Para obtener más información, vea [Instalar SQL Server 2014 desde el símbolo del sistema](install-sql-server-from-the-command-prompt.md).  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] no se puede instalar en paralelo con versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un equipo que ejecute [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 o [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core.  
  
 Con independencia del método de instalación, es necesario confirmar la aceptación de los términos de la licencia de software como usuario individual o en nombre de una entidad, a menos que el uso del software en su caso se rija por un acuerdo independiente, como un acuerdo de licencia por volumen de [!INCLUDE[msCoName](../../includes/msconame-md.md)] o un acuerdo suscrito con un ISV u OEM.  
  
 Los términos de la licencia se muestran para revisarlos y aceptarlos en la interfaz de usuario del programa de instalación. Las instalaciones desatendidas (mediante los parámetros /Q o /QS) deben incluir el parámetro /IACCEPTSQLSERVERLICENSETERMS. Puede revisar separadamente los términos de licencia en [Términos de licencia de software de Microsoft](https://go.microsoft.com/fwlink/?LinkId=148209).  
  
> [!NOTE]  
>  En función de cómo haya recibido el software (por ejemplo, a través de un contrato de licencias por volumen de [!INCLUDE[msCoName](../../includes/msconame-md.md)] ), su uso del software puede estar sujeto a términos y condiciones adicionales.  
  
 Para instalar características específicas, use el parámetro /FEATURES y especifique la característica primaria o los valores de las características. Para obtener más información sobre los parámetros de las características y su uso, consulte las siguientes secciones.  
  
### <a name="feature-parameters"></a>Parámetros de características  
  
|Parámetro de característica|Descripción|  
|-----------------------|-----------------|  
|SQLENGINE|Instala solo el [!INCLUDE[ssDE](../../includes/ssde-md.md)].|  
|REPLICACIÓN|Instala el componente Replicación junto con [!INCLUDE[ssDE](../../includes/ssde-md.md)].|  
|FULLTEXT|Instala el componente Texto completo junto con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].|  
|AS|Instala todos los componentes de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|IS|Instala todos los componentes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|CONN|Instala los componentes de conectividad.|  
  
 Vea los siguientes ejemplos de uso de los parámetros de la característica:  
  
|Parámetro y valores|Descripción|  
|--------------------------|-----------------|  
|/FEATURES=SQLEngine|Instala solo el [!INCLUDE[ssDE](../../includes/ssde-md.md)].|  
|/FEATURES=SQLEngine,FullText|Instala [!INCLUDE[ssDE](../../includes/ssde-md.md)] y Texto completo.|  
|/FEATURES=SQLEngine,Conn|Instala los componentes de conectividad y [!INCLUDE[ssDE](../../includes/ssde-md.md)] .|  
|/FEATURES=SQLEngine,AS,IS,Conn|Instala el [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]y los componentes de conectividad.|  
  
### <a name="installation-options"></a>Opción de instalación  
 El programa de instalación admite las opciones de instalación siguientes al instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] en un sistema operativo Server Core:  
  
1.  **Instalación desde la línea de comandos**  
  
     Para instalar características específicas mediante la opción de instalación del símbolo del sistema, use el parámetro /FEATURES y especifique la característica principal o los valores de la característica. El siguiente es un ejemplo del uso de los parámetros de la línea de comandos:  
  
    ```cmd
    setup.exe /qs /ACTION=Install /FEATURES=SQLEngine,Replication /INSTANCENAME=MSSQLSERVER /SQLSVCACCOUNT="<DomainName\UserName>" /SQLSVCPASSWORD="<StrongPassword>" /SQLSYSADMINACCOUNTS="<DomainName\UserName>" /AGTSVCACCOUNT="NT AUTHORITY\Network Service" /TCPENABLED=1 /IACCEPTSQLSERVERLICENSETERMS  
    ```  
  
2.  **Instalación mediante el archivo de configuración**  
  
     El programa de instalación admite el uso del archivo de configuración solamente a través del símbolo del sistema. El archivo de configuración es un archivo de texto con la estructura básica de un parámetro (pares nombre-valor) y un comentario descriptivo. El archivo de configuración especificado en el símbolo del sistema debe tener una extensión de nombre de archivo .INI. Vea los ejemplos siguientes de ConfigurationFile.INI:  
  
    -   Instalación de [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
         En el siguiente ejemplo se muestra cómo instalar una nueva instancia independiente que incluye el [!INCLUDE[ssDE](../../includes/ssde-md.md)] de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
        ```  
        ; ssNoVersion Configuration File  
        [OPTIONS]  
  
        ; Specifies a Setup work flow, like INSTALL, UNINSTALL, or UPGRADE. This is a required parameter.   
  
        ACTION="Install"  
  
        ; Specifies features to install, uninstall, or upgrade. The lists of features include SQLEngine, FullText, Replication, AS, IS, and Conn.   
  
        FEATURES=SQLENGINE  
  
        ; Specify a default or named instance. MSSQLSERVER is the default instance for non-Express editions and SQLExpress for Express editions. This parameter is required when installing the ssNoVersion Database Engine, and Analysis Services (AS).  
  
        INSTANCENAME="MSSQLSERVER"  
  
        ; Specify the Instance ID for the ssNoVersion features you have specified. ssNoVersion directory structure, registry structure, and service names will incorporate the instance ID of the ssNoVersion instance.   
  
        INSTANCEID="MSSQLSERVER"  
  
        ; Account for ssNoVersion service: Domain\User or system account.   
  
        SQLSVCACCOUNT="NT Service\MSSQLSERVER"  
  
        ; Windows account(s) to provision as ssNoVersion system administrators.   
  
        SQLSYSADMINACCOUNTS="<DomainName\UserName>"  
  
        ; Accept the License agreement to continue with Installation  
  
        IAcceptSQLServerLicenseTerms="True"
        ```  
  
    -   Instalar los componentes de conectividad  
  
         En el siguiente ejemplo se muestra cómo instalar los componentes de conectividad:  
  
        ```  
        ; ssNoVersion Configuration File  
        [OPTIONS]  
  
        ; Specifies a Setup work flow, like INSTALL, UNINSTALL, or UPGRADE. This is a required parameter.   
  
        ACTION="Install"  
  
        ; Specifies features to install, uninstall, or upgrade. The lists of features include SQLEngine, FullText, Replication, AS, IS, and Conn.   
  
        FEATURES=Conn  
  
        ; Specifies acceptance of License Terms  
  
        IAcceptSQLServerLicenseTerms="True
        ```  
  
    -   Instalar todas las características compatibles  
  
         En el siguiente ejemplo se muestra cómo instalar todas las características admitidas de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] en Server Core:  
  
        ```  
        ; ssNoVersion Configuration File  
        [OPTIONS]  
        ; Specifies a Setup work flow, like INSTALL, UNINSTALL, or UPGRADE. This is a required parameter.   
  
        ACTION="Install"  
  
        ; Specifies features to install, uninstall, or upgrade. The lists of features include SQLEngine, FullText, Replication, AS, IS, and Conn.   
  
        FEATURES=SQLENGINE,FullText,Replication,AS,IS,Conn  
  
        ; Specify a default or named instance. MSSQLSERVER is the default instance for non-Express editions and SQLExpress for Express editions. This parameter is required when installing the ssNoVersion Database Engine (SQL), or Analysis Services (AS).  
  
        INSTANCENAME="MSSQLSERVER"  
  
        ; Specify the Instance ID for the ssNoVersion features you have specified. ssNoVersion directory structure, registry structure, and service names will incorporate the instance ID of the ssNoVersion instance.   
  
        INSTANCEID="MSSQLSERVER"  
  
        ; Account for ssNoVersion service: Domain\User or system account.   
  
        SQLSVCACCOUNT="NT Service\MSSQLSERVER"  
  
        ; Windows account(s) to provision as ssNoVersion system administrators.   
  
        SQLSYSADMINACCOUNTS="<DomainName\UserName>"  
  
        ; The name of the account that the Analysis Services service runs under.   
  
        ASSVCACCOUNT= "NT Service\MSSQLServerOLAPService"  
  
        ; Specifies the list of administrator accounts that need to be provisioned.   
  
        ASSYSADMINACCOUNTS="<DomainName\UserName>"  
  
        ; Specifies the server mode of the Analysis Services instance. Valid values are MULTIDIMENSIONAL, POWERPIVOT or TABULAR. ASSERVERMODE is case-sensitive. All values must be expressed in upper case.   
  
        ASSERVERMODE="MULTIDIMENSIONAL"  
  
        ; Optional value, which specifies the state of the TCP protocol for the ssNoVersion service. Supported values are: 0 to disable the TCP protocol, and 1 to enable the TCP protocol.  
  
        TCPENABLED=1  
  
        ;Specifies acceptance of License Terms  
  
        IAcceptSQLServerLicenseTerms="True"  
        ```  
  
     En los ejemplos siguientes se muestra cómo puede iniciar la instalación mediante un archivo de configuración.  
  
    -   Archivo de configuración  
  
         A continuación se ofrecen algunos ejemplos de uso del archivo de configuración:  
  
        -   Para especificar el archivo de configuración en el símbolo del sistema:  
  
        ```cmd
        setup.exe /QS /ConfigurationFile=MyConfigurationFile.INI  
        ```  
  
        -   Para especificar las contraseñas en el símbolo del sistema en lugar de hacerlo en el archivo de configuración:  
  
        ```cmd
        setup.exe /QS /SQLSVCPASSWORD="************" /ASSVCPASSWORD="************"  /ConfigurationFile=MyConfigurationFile.INI  
        ```  
  
    -   DefaultSetup.ini  
  
         Si tiene el archivo DefaultSetup.ini en las carpetas \x86 y \x64 en el nivel raíz del medio de origen de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , abra el archivo DefaultSetup.ini y agregue el parámetro *Features* al archivo.  
  
         Si el archivo DefaultSetup.ini no existe, puede crearlo y copiarlo a las carpetas \x86 y \x64 en el nivel raíz de la ubicación de origen de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="configuring-remote-access-of-ssnoversion-running-on-server-core"></a>Configurar el acceso remoto de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en ejecución en Server Core  
 Realice las acciones descritas a continuación para configurar el acceso remoto de una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] que se está ejecutando en una instalación Server Core de [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1 o [!INCLUDE[win8srv](../../includes/win8srv-md.md)].  
  
### <a name="enable-remote-connections-on-the-instance-of-ssnoversion"></a>Habilitar las conexiones remotas en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Para habilitar las conexiones remotas, use SQLCMD.exe localmente y ejecute las instrucciones siguientes en la instancia de Server Core:  
  
-   `EXEC sys.sp_configure N'remote access', N'1'`  
  
     `GO`  
  
-   `RECONFIGURE WITH OVERRIDE`  
  
     `GO`  
  
### <a name="enable-and-start-the-ssnoversion-browser-service"></a>Habilitar e iniciar el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser  
 De forma predeterminada, el servicio Explorer se deshabilita.  Si se deshabilita en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se ejecuta en Server Core, ejecute el siguiente comando desde el símbolo del sistema para habilitarlo:  
  
 `sc config SQLBROWSER start= auto`  
  
 Una vez habilitado, ejecute el siguiente comando desde el símbolo del sistema para iniciar el servicio:  
  
 `net start SQLBROWSER`  
  
### <a name="create-exceptions-in-windows-firewall"></a>Crear excepciones en Firewall de Windows  
 Para crear excepciones para el acceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en Firewall de Windows, siga los pasos especificados en [Configurar Firewall de Windows para permitir el acceso a SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
### <a name="enable-tcpip-on-the-instance-of-ssnoversion"></a>Habilitar TCP/IP en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 El protocolo TCP/IP puede habilitarse a través de Windows PowerShell para una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en Server Core. Siga estos pasos:  
  
1.  En el equipo que ejecuta [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 o [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core, inicie el Administrador de tareas.  
  
2.  En la pestaña **Aplicaciones** , haga clic en **Nueva tarea**.  
  
3.  En el cuadro de diálogo **Crear nueva tarea** , escriba **sqlps.exe** en el campo **Abrir** y, a continuación, haga clic en **Aceptar**. Se abrirá la ventana de ** [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell** .  
  
4.  En la ventana **Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Powershell**, ejecute el siguiente script para habilitar el protocolo TCP/IP:  
  
```powershell
$smo = 'Microsoft.SqlServer.Management.Smo.'  
$wmi = New-Object ($smo + 'Wmi.ManagedComputer')  
# Enable the TCP protocol on the default instance.  If the instance is named, replace MSSQLSERVER with the instance name in the following line.  
$uri = "ManagedComputer[@Name='" + (get-item env:\computername).Value + "']/ServerInstance[@Name='MSSQLSERVER']/ServerProtocol[@Name='Tcp']"  
$Tcp = $wmi.GetSmoObject($uri)  
$Tcp.IsEnabled = $true  
$Tcp.Alter()  
$Tcp  
```  
  
## <a name="uninstallation"></a>Desinstalación  
 Después de iniciar sesión en un equipo que ejecute [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] Server Core SP1 o [!INCLUDE[win8srv](../../includes/win8srv-md.md)] Server Core, tiene un entorno de escritorio limitado con un símbolo del sistema del administrador. Puede utilizar este símbolo del sistema para iniciar la desinstalación de una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para desinstalar una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], inicie la desinstalación desde el símbolo del sistema el modo completamente silencioso utilizando el parámetro /Q o en modo silencioso simple utilizando el parámetro /QS. El parámetro /QS muestra el progreso a través de la interfaz de usuario, pero no acepta ninguna entrada. /Q se ejecuta en modo silencioso sin ninguna interfaz de usuario.  
  
 Para desinstalar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]existente.  
  
```cmd
setup.exe /Q /Action=Uninstall /FEATURES=SQLEngine,AS,IS /INSTANCENAME=MSSQLSERVER  
```  
  
 Para quitar una instancia con nombre, especifique el nombre de la instancia en lugar de "MSSQLSERVER" en el ejemplo anterior.  
  
> [!WARNING]
>  Si cierra el símbolo del sistema accidentalmente, puede iniciar un nuevo símbolo del sistema siguiendo estos pasos:  
> 
>  1.  Presione Ctrl+Mayús+Esc para mostrar el Administrador de tareas.  
> 2.  En la pestaña **Aplicaciones** , haga clic en **Nueva tarea**.  
> 3.  En el cuadro de diálogo **Crear nueva tarea** , escriba **cmd** en el campo **Abrir** y haga clic en [!INCLUDE[clickOK](../../includes/clickok-md.md)].  
  
## <a name="see-also"></a>Consulte también  
 [Instalación de SQL Server 2014 mediante un archivo de configuración](install-sql-server-using-a-configuration-file.md)   
 [Instalación de SQL Server 2014 desde el símbolo del sistema](install-sql-server-from-the-command-prompt.md)   
 [Características admitidas por las ediciones de SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [Guía Introducción de la opción de instalación Server Core](https://go.microsoft.com/fwlink/?LinkId=221422)   
 [Configuración de una instalación de Server Core: información general](https://go.microsoft.com/fwlink/?LinkId=221423)   
 [Cmdlets de clúster de conmutación por error en Windows PowerShell enumerados por tarea](https://go.microsoft.com/fwlink/?LinkId=221419)   
 [Mapping Cluster.exe Commands to Windows PowerShell Cmdlets for Failover Clusters (Asignación de comandos cluster.exe a cmdlets de Windows PowerShell para clústeres de conmutación por error)](https://go.microsoft.com/fwlink/?LinkId=221421)  
