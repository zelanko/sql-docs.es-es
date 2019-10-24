---
title: Analysis Services PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 03/11/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 60bb9610-7229-42eb-a95f-a377268a8720
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: f75298a4701f15a1fc0f3f471bf7628f4a7030c1
ms.sourcegitcommit: a165052c789a327a3a7202872669ce039bd9e495
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/22/2019
ms.locfileid: "72782649"
---
# <a name="analysis-services-powershell"></a>Analysis Services PowerShell
  [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] incluye cmdlets y un proveedor de Analysis Services PowerShell (SQLAS) que permite usar Windows PowerShell para navegar, administrar y consultar objetos de Analysis Services.  
  
 Analysis Services PowerShell consta de:  
  
-   Un proveedor de `SQLAS` que se usa para navegar por la jerarquía de Objetos de administración de análisis (AMO).  
  
-   El cmdlet `Invoke-ASCmd` que se utiliza para ejecutar script XMLA, MDX o DMX.  
  
-   Cmdlets específicos de la tarea para ejecuciones rutinarias, como el procesamiento, la administración de roles, la administración de particiones, las copias de seguridad y la restauración.  
  
## <a name="in-this-article"></a>En este artículo  
 [Requisitos previos](#bkmk_prereq)  
  
 [Versiones admitidas y modos de Analysis Services](#bkmk_vers)  
  
 [Requisitos de autenticación y consideraciones de seguridad](#bkmk_auth)  
  
 [Analysis Services tareas de PowerShell](#bkmk_tasks)  

Para obtener más información sobre la sintaxis y los ejemplos, vea [Analysis Services referencia de PowerShell](/sql/analysis-services/powershell/analysis-services-powershell-reference).

##  <a name="bkmk_prereq"></a> Prerequisites  
 Windows PowerShell 2.0 debe estar instalado. Se instaló de forma predeterminada en las versiones más recientes de los sistemas operativos Windows. Para obtener más información, vea [instalar Windows PowerShell 2,0](https://msdn.microsoft.com/library/ff637750.aspx)

<!-- ff637750.aspx above is linked to by:  (https://go.microsoft.com/fwlink/?LinkId=227613). -->
  
 Debe instalar una característica de SQL Server que incluya el módulo SQL Server PowerShell (SQLPS) y las bibliotecas de cliente. La manera más fácil de hacerlo es instalar SQL Server Management Studio, que incluye automáticamente la característica PowerShell y las bibliotecas de cliente. El módulo SQL Server PowerShell (SQLPS) contiene los proveedores y cmdlets de PowerShell para todas las características de SQL Server, incluido el módulo SQLASCmdlets y el proveedor SQLAS utilizados para navegar por la jerarquía de objetos de Analysis Services.  
  
 Debe importar el módulo **SQLPS** para poder usar los cmdlets y el proveedor de `SQLAS`. El proveedor SQLAS es una extensión del proveedor de `SQLServer`. Hay varias maneras de importar el módulo SQLPS. Para más información, vea [Importar el módulo SQLPS](../../2014/database-engine/import-the-sqlps-module.md).  
  
 El acceso remoto a una instancia de Analysis Services requiere que habilite la administración remota y el uso compartido de archivos. Para obtener más información, consulte [Habilitar la administración remota](#bkmk_remote) en este tema.  
  
##  <a name="bkmk_vers"></a> Versiones admitidas y modos de Analysis Services  
 Actualmente, Analysis Services PowerShell se admite en cualquier edición de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Analysis Services que se ejecuta en Windows Server 2008 R2, Windows Server 2008 SP1 o Windows 7.  
  
 En la tabla siguiente es muestra la disponibilidad de Analysis Services PowerShell en varios contextos.  
  
|Contexto|Disponibilidad de las características de PowerShell|  
|-------------|-------------------------------------|  
|Bases de datos e instancias multidimensionales|Se admite para la administración remota y local.<br /><br /> Merge-partition requiere una conexión local.|  
|Bases de datos e instancias tabulares|Se admite para la administración remota y local.<br /><br /> Para obtener más información, consulte un blog de agosto de 2011 sobre la [Administración de modelos tabulares con PowerShell](https://go.microsoft.com/fwlink/?linkID=227685).|  
|Bases de datos e instancias de PowerPivot para SharePoint|Compatibilidad limitada. Puede utilizar las conexiones HTTP y el proveedor SQLAS para ver información de las bases de datos y las instancias.<br /><br /> Sin embargo, no se admite el uso de los cmdlets. No debe utilizar Analysis Services PowerShell para las copias de seguridad y restauración de bases de datos PowerPivot en memoria, ni debe agregar o quitar roles, procesar datos o ejecutar script XMLA arbitrario.<br /><br /> Para la configuración, PowerPivot para SharePoint tiene una compatibilidad integrada con PowerShell que se proporciona por separado. Para obtener más información, vea [referencia de PowerShell para PowerPivot para SharePoint](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint).|  
|Conexiones nativas a cubos locales<br /><br /> "Data Source = c:\backup\test.Cub"|No admitido.|  
|Conexiones HTTP a archivos de conexión de modelos semánticos BI (.bism) en SharePoint<br /><br /> "Data Source =http://server/shared_docs/name.bism"|No admitido.|  
|Conexiones incrustadas a bases de datos PowerPivot<br /><br /> "Data Source = $Embedded $"|No admitido.|  
|Contexto del servidor local en los procedimientos almacenados de Analysis Services<br /><br /> "Data Source = *"|No admitido.|  
  
##  <a name="bkmk_auth"></a>Requisitos de autenticación y consideraciones de seguridad  
 Al conectarse a Analysis Services, debe realizar la conexión utilizando una identidad de usuario de Windows. En su mayor parte, una conexión se realiza utilizando la seguridad integrada de Windows, donde la identidad del usuario actual establece el contexto de seguridad en el que se realizan las operaciones de servidor. Sin embargo, están disponibles métodos de autenticación adicionales cuando se configura el acceso a Analysis Services a través de HTTP. En esta sección se explica cómo el tipo de conexión determina qué opciones de autenticación se pueden usar.  
  
 Las conexiones a Analysis Services se caracterizan como conexiones nativas o conexiones HTTP. Una conexión nativa es una conexión directa de una aplicación cliente con el servidor. En una sesión de PowerShell, el cliente de PowerShell utiliza el proveedor OLE DB para la conexión directa de Analysis Services con una instancia de Analysis Services. Una conexión nativa se realiza siempre utilizando la seguridad integrada de Windows, donde Analysis Services PowerShell se ejecuta como el usuario actual. Analysis Services no admite la suplantación. Si desea realizar una operación como un usuario específico, debe iniciar la sesión de PowerShell como ese usuario.  
  
 Las conexiones HTTP se realizan indirectamente a través de IIS, permitiendo opciones adicionales de autenticación, como la autenticación básica, para conectarse a una instancia de Analysis Services. Como IIS admite la suplantación, se puede proporcionar una cadena de conexión que incluya credenciales que IIS utilizará para realizar la suplantación cuando se realice una conexión. Para proporcionar credenciales, puede usar el parámetro-Credential.  
  
 **Usar el parámetro-credential en PowerShell**  
  
 El parámetro-credential toma un objeto PSCredential que especifica un nombre de usuario y una contraseña. En Analysis Services PowerShell, el parámetro-credential está disponible para los cmdlets que realizan una solicitud de conexión a Analysis Services, en lugar de a los cmdlets que se ejecutan en el contexto de una conexión existente. Entre los cmdlets que realizan una solicitud de conexión se hallan Invoke-ASCmd, Backup-ASDatabase y Restore-ASDatabase. Para estos cmdlets, se puede usar el parámetro-Credential, siempre que se cumplan los siguientes criterios:  
  
1.  El servidor se configura para el acceso a través de HTTP, lo que significa que IIS administra la conexión, lee el nombre de usuario y la contraseña, y suplanta la identidad del usuario al conectarse a Analysis Services. Para obtener más información, vea [Configurar el acceso HTTP a Analysis Services en Internet Information Services &#40;IIS&#41; 8.0](instances/configure-http-access-to-analysis-services-on-iis-8-0.md).  
  
2.  El directorio virtual de IIS creado para el acceso a Analysis Services a través de HTTP se configura para la autenticación básica.  
  
3.  El nombre de usuario y la contraseña proporcionados por el objeto de credencial se resuelve como una identidad de usuario de Windows. Analysis Services utiliza esta identidad como usuario actual. Si el usuario no es un usuario de Windows, o carece de los permisos suficientes para realizar la operación solicitada, la solicitud dará un error.  
  
 Para crear un objeto de credencial, puede utilizar el cmdlet Get-Credential para recopilar las credenciales del operador. A continuación, puede utilizar el objeto de credencial en un comando que realiza la conexión a Analysis Services. En el ejemplo siguiente se muestra un enfoque. En este ejemplo, la conexión es a una instancia local (`SQLSERVER:\SQLAS\HTTP_DS`) configurada para el acceso HTTP.  
  
```powershell
$cred = Get-Credential adventureworks\dbadmin  
Invoke-ASCmd -Inputfile:"c:\discoverconnections.xmla" -Credential:$cred  
```  
  
 Cuando se utiliza la autenticación básica, debe utilizar siempre HTTPS con SSL para que el nombre de usuario y las contraseñas se envíen mediante una conexión cifrada. Para obtener más información, vea [configurar capa de sockets seguros en iis 7,0](https://go.microsoft.com/fwlink/?linkID=184299) y [configurar la autenticación básica (IIS 7)](https://go.microsoft.com/fwlink/?LinkId=230776).  
  
 Recuerde que las credenciales, las consultas, y los comandos que se proporcionan en PowerShell se pasan sin cambiar a la capa de transporte. La inclusión de contenido confidencial en los scripts aumenta el riesgo de un ataque malintencionado por inyección.  
  
 **Proporcionar una contraseña como un objeto Microsoft. Secure. String**  
  
 Algunas operaciones, como copias de seguridad y restauración, admiten opciones de cifrado que se activan al proporcionar una contraseña en el comando. La acción de proporcionar la contraseña indica a Analysis Services que se ha de cifrar o descifrar el archivo de copia de seguridad. En Analysis Services, se crea una instancia de esta contraseña como un objeto de cadena seguro. En el ejemplo siguiente se proporciona una ilustración de cómo se recopila una contraseña del operador en tiempo de ejecución.  
  
```powershell
$pwd = read-host -AsSecureString -Prompt "Password"  
$pwd -is [System.IDisposable]  
```  
  
 Ahora puede realizar una operación de copia de seguridad o de restauración en un archivo de base de datos cifrado pasando la variable $pwd al parámetro de contraseña. Para ver un ejemplo completo que combina esta ilustración con otros cmdlets, consulte [cmdlet backup-asdatabase](/powershell/module/sqlserver/backup-asdatabase) y [cmdlet restore-asdatabase](/powershell/module/sqlserver/restore-asdatabase).
  
 Como paso de seguimiento, quite de la sesión tanto la contraseña como la variable.  
  
```powershell
$pwd.Dispose()  
Remove-Variable -Name pwd  
```  
  
##  <a name="bkmk_tasks"></a>Analysis Services tareas de PowerShell  
 Puede ejecutar Analysis Services PowerShell desde el shell de administración de Windows PowerShell o desde un símbolo del sistema de Windows. No se admite la ejecución de Analysis Services PowerShell desde [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
 En esta sección se describen las tareas comunes para utilizar Analysis Services PowerShell.  
  
-   [Cargar el proveedor de Analysis Services y los cmdlets](#bkmk_load)  
  
-   [Habilitar la administración remota](#bkmk_remote)  
  
-   [Conexión a un objeto Analysis Services](#bkmk_connect)  
  
-   [Administrar el servicio](#bkmk_admin)  
  
-   [Obtención de ayuda para Analysis Services PowerShell](#bkmk_help)  
  
###  <a name="bkmk_load"></a>Cargar el proveedor de Analysis Services y los cmdlets  
 El proveedor de Analysis Services es una extensión del proveedor raíz de SQL Server que está disponible al importar el módulo SQLPS. Los cmdlets de Analysis Services se cargan simultáneamente; también puede cargarlos de modo independiente si desea utilizarlos con el proveedor.  
  
-   Ejecute el cmdlet del módulo Import para cargar el SQLPS que incluye toda la funcionalidad de Analysis Services PowerShell. Si no puede importar el módulo, puede cambiar temporalmente la directiva de ejecución a unrestricted con el fin de cargar el módulo. Para más información, vea [Importar el módulo SQLPS](../../2014/database-engine/import-the-sqlps-module.md).  
  
    ```powershell
    Import-Module "sqlps"  
    ```  
  
     O bien, use `import-module "sqlps" -disablenamechecking` para quitar la advertencia sobre los nombres de verbo no aprobados.  
  
-   Para cargar solo los cmdlets de Analysis Services específicos de la tarea, sin el proveedor de Analysis Services o el cmdlet Invoke-ASCmd, puede cargar el módulo SQLASCmdlets como una operación independiente.  
  
    ```powershell
    Import-Module "sqlascmdlets"  
    ```  
  
###  <a name="bkmk_remote"></a>Habilitar la administración remota  
 Para poder utilizar Analysis Services PowerShell con una instancia remota de Analysis Services, primero debe habilitar la administración remota y el uso compartido de archivos. El siguiente error indica un problema de configuración del firewall: "el servidor RPC no está disponible. (Excepción de HRESULT: 0x800706BA)”.  
  
1.  Compruebe que el equipo local y los equipos remotos tienen las versiones de [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] de las herramientas de servidor y de cliente.  
  
2.  En el servidor remoto que hospeda una instancia de Analysis Services, abra el puerto TCP 2383 en Firewall de Windows. Si instaló Analysis Services como una instancia con nombre o con un puerto personalizado, el número de puerto será diferente. Para obtener más información, consulte [Configure the Windows Firewall to Allow Analysis Services Access](instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
3.  En el servidor remoto, compruebe que los siguientes servicios se han iniciado: servicio Llamada a procedimiento remoto (RPC), servicio del asistente NetBIOS TCP/IP, servicio Instrumental de administración de Windows (WMI), Servicio de administración remota de Windows (WS-Management).  
  
4.  En el servidor remoto, inicie el complemento Editor de objetos de directiva de grupo (gpedit.msc).  
  
5.  Abra sucesivamente Configuración del equipo, Plantillas administrativas, Red, Conexiones de red,Firewall de Windows y, por último, Perfil de dominio.  
  
6.  Haga doble clic en **firewall de Windows: permitir excepción de administración remota entrante**, seleccione **habilitado**y, a continuación, haga clic en **Aceptar**.  
  
7.  Haga doble clic en **firewall de Windows: permitir excepción de compartir archivos e impresoras entrantes**, seleccione **habilitado**y, a continuación, haga clic en **Aceptar**.  
  
8.  En el equipo local que tiene las herramientas cliente, use los cmdlets siguientes para comprobar la administración remota, sustituyendo el nombre de servidor real por el marcador de posición de *nombre de servidor remoto* . Omita el nombre de instancia si Analysis Services se instala como la instancia predeterminada. Debe haber importado previamente el módulo SQLPS para que el comando funcione.  
  
    ```
    PS SQLSERVER:\> cd sqlas
    PS SQLSERVER:\sqlas> cd <remote-server-name\instance-name>  
    PS SQLSERVER:\sqlas\<remote-server-name\instance-name> dir  
    ```  
  
 En algunos casos, es posible que sea necesaria una configuración adicional. Puede que tenga que escribir lo siguiente en el servidor remoto para poderle emitir comandos desde otro equipo:  
  
```powershell
Enable-PSRemoting  
```  
  
  
###  <a name="bkmk_connect"></a>Conexión a un objeto Analysis Services  
 El proveedor de Analysis Services PowerShell admite la navegación de la jerarquía de objetos de Analysis Services y establece el contexto para los comandos en ejecución. El proveedor es una extensión del proveedor raíz de SQLSERVER disponible a través del módulo SQLPS. Después de cargar el módulo SQLPS, puede navegar por la ruta de acceso.  
  
 Puede conectarse a una instancia local o remota, pero algunos cmdlets solo se pueden ejecutar en una instancia local (a saber, merge-partition). Puede utilizar una conexión nativa o una conexión HTTP para los servidores de Analysis Services que configuró para el acceso HTTP. En las ilustraciones siguientes se muestra la ruta de acceso de navegación de las conexiones HTTP y nativas. En las ilustraciones siguientes se muestra la ruta de acceso de navegación de las conexiones HTTP y nativas.  
  
 **Conexiones nativas a Analysis Services**  
  
 ![Conexión nativa a Analysis Services](media/ssas-powershell-nativeconnection.gif "Conexión nativa a Analysis Services")  
  
 El ejemplo siguiente es una demostración de cómo utilizar una conexión nativa para navegar por la jerarquía de objetos. Desde el proveedor, puede emitir un `dir` para ver la información de la instancia. Puede utilizar `cd` para ver los objetos de esa instancia.  
  
```  
PS SQLSERVER:> cd sqlas  
PS SQLSERVER\sqlas:> dir  
PS SQLSERVER\sqlas:> cd localhost\default  
PS SQLSERVER\sqlas\localhost\default:> dir  
```  
  
 Debe ver las colecciones siguientes: ensamblados, bases de datos, roles y seguimientos. Si continúa utilizando `cd` y `dir`, puede ver el contenido de cada colección.  
  
 **Conexiones HTTP a Analysis Services**  
  
 ![Conexión HTTP a Analysis Services](media/ssas-powershell-httpconnection.gif "Conexión HTTP a Analysis Services")  
  
 Las conexiones HTTP son útiles si ha configurado el servidor para el acceso HTTP siguiendo las instrucciones de este tema: [Configure http Access to &#40;Analysis Services&#41; on Internet Information Services IIS 8,0](instances/configure-http-access-to-analysis-services-on-iis-8-0.md)  
  
 Suponiendo una dirección URL de servidor de http://localhost/olap/msmdpump.dll, una conexión podría ser similar a la siguiente:  
  
```  
PS SQLSERVER\sqlas:> cd http_ds  
PS SQLSERVER\sqlas\http_ds:> $Url=Encode-SqlName "http://localhost/olap/msmdpump.dll"  
PS SQLSERVER\sqlas\http_ds:> cd $Url  
PS SQLSERVER\sqlas\http_ds\http%3A%2F%2Flocalhost%2olap%2msmdpump%2Edll:> dir  
```  
  
 Debe ver las colecciones siguientes: ensamblados, bases de datos, roles y seguimientos. Si no puede ver el contenido de estas colecciones, compruebe la configuración de la autenticación en el directorio virtual OLAP. Asegúrese de que el acceso anónimo está deshabilitado. Si utiliza la autenticación de Windows, asegúrese de que la cuenta de usuario de Windows tiene permisos administrativos en la instancia de Analysis Services.  
  
###  <a name="bkmk_admin"></a>Administrar el servicio  
 Compruebe que el servicio se está ejecutando. Devuelve el estado, el nombre y el nombre para mostrar de servicios de SQL Server, incluido Analysis Services (MSSQLServerOLAPService) y el motor de base de datos.  
  
```powershell
Get-Service mssql*  
```  
  
 Devuelve las propiedades de un proceso, incluido el identificador de proceso, el recuento de identificadores y el uso de memoria:  
  
```powershell
Get-Process msmdsrv  
```  
  
 Reinicia el servicio al emitir el cmdlet siguiente desde el shell de administración:  
  
```powershell
Restart-Service mssqlserverolapservice  
```  
  
###  <a name="bkmk_help"></a>Obtención de ayuda para Analysis Services PowerShell  
 Use cualquiera de los siguientes cmdlets para comprobar su disponibilidad y obtener más información acerca de los servicios, los procesos y los objetos.  
  
1.  `Get-Help` devuelve la Ayuda integrada para un cmdlet de Analysis Services, incluidos los ejemplos:  
  
    ```powershell
    Get-Help invoke-ascmd -Examples  
    ```  
  
2.  `Get-Command` devuelve una lista de los once cmdlets de Analysis Services PowerShell:  
  
    ```powershell
    Get-Command -module SQLASCmdlets  
    ```  
  
3.  `Get-Member` devuelve las propiedades o los métodos de un servicio o un proceso.  
  
    ```powershell
    Get-Service mssqlserverolapservice | Get-Member -Type Property  
    ```  
  
    ```powershell
    Get-Service mssqlserverolapservice | Get-Member -Type Method  
    ```  
  
    ```powershell
    Get-Process msmdsrv | Get-Member -Type Property  
    ```  
  
4.  `Get-Member` también se puede utilizar para devolver las propiedades o los métodos de un objeto (por ejemplo, los métodos AMO en el objeto de servidor) mediante el proveedor SQLAS para especificar la instancia de servidor.  
  
    ```
    PS SQLSERVER:\sqlas\localhost\default > $serverObj = New-Object Microsoft.AnalysisServices.Server  
    PS SQLSERVER:\sqlas\localhost\default > $serverObj = | Get-Member -Type Method  
    ```  
  
5.  `Get-PSdrive` devuelve una lista de los proveedores instalados actualmente. Si importó el módulo SQLPS, verá el proveedor `SQLServer` en la lista (SQLAS forma parte del proveedor SQLServer y nunca aparece de forma independiente en la lista):  
  
    ```powershell
    Get-PSDrive  
    ```  
  
## <a name="see-also"></a>Ver también  
 [Instalar SQL Server PowerShell](../database-engine/install-windows/install-sql-server-powershell.md)   
 [Administrar modelos tabulares con PowerShell (blog)](https://go.microsoft.com/fwlink/?linkID=227685)   
 [Configurar el acceso HTTP a Analysis Services en Internet Information Services &#40;IIS&#41; 8.0](instances/configure-http-access-to-analysis-services-on-iis-8-0.md)  
  
  
