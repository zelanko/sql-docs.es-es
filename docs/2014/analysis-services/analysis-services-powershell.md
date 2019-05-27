---
title: PowerShell de Analysis Services | Microsoft Docs
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
ms.openlocfilehash: e3c8eda71783e7211011bd6f67d9acf638c8946a
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66062520"
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
  
 [Tareas de PowerShell de Analysis Services](#bkmk_tasks)  

Para obtener más información sobre sintaxis y ejemplos, vea [Analysis Services PowerShell Reference](/sql/analysis-services/powershell/analysis-services-powershell-reference).

##  <a name="bkmk_prereq"></a> Requisitos previos  
 Windows PowerShell 2.0 debe estar instalado. Se instaló de forma predeterminada en las versiones más recientes de los sistemas operativos Windows. Para obtener más información, consulte [instalar Windows PowerShell 2.0](https://msdn.microsoft.com/library/ff637750.aspx)

<!-- ff637750.aspx above is linked to by:  (https://go.microsoft.com/fwlink/?LinkId=227613). -->
  
 Debe instalar una característica de SQL Server que incluya el módulo SQL Server PowerShell (SQLPS) y las bibliotecas de cliente. La manera más fácil de hacerlo es instalar SQL Server Management Studio, que incluye automáticamente la característica PowerShell y las bibliotecas de cliente. El módulo SQL Server PowerShell (SQLPS) contiene los proveedores y cmdlets de PowerShell para todas las características de SQL Server, incluido el módulo SQLASCmdlets y el proveedor SQLAS utilizados para navegar por la jerarquía de objetos de Analysis Services.  
  
 Debe importar el **SQLPS** módulo antes de poder usar el `SQLAS` proveedor y los cmdlets. El proveedor SQLAS es una extensión de la `SQLServer` proveedor. Hay varias maneras de importar el módulo SQLPS. Para más información, vea [Importar el módulo SQLPS](../../2014/database-engine/import-the-sqlps-module.md).  
  
 El acceso remoto a una instancia de Analysis Services requiere que habilite la administración remota y el uso compartido de archivos. Para obtener más información, consulte [Habilitar administración remota](#bkmk_remote) en este tema.  
  
##  <a name="bkmk_vers"></a> Versiones admitidas y modos de Analysis Services  
 Actualmente, Analysis Services PowerShell se admite en cualquier edición de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] Analysis Services que se ejecuta en Windows Server 2008 R2, Windows Server 2008 SP1 o Windows 7.  
  
 En la tabla siguiente es muestra la disponibilidad de Analysis Services PowerShell en varios contextos.  
  
|Contexto|Disponibilidad de las características de PowerShell|  
|-------------|-------------------------------------|  
|Bases de datos e instancias multidimensionales|Se admite para la administración remota y local.<br /><br /> Merge-partition requiere una conexión local.|  
|Bases de datos e instancias tabulares|Se admite para la administración remota y local.<br /><br /> Para obtener más información, vea un blog de agosto de 2011 [administrar modelos tabulares con PowerShell](https://go.microsoft.com/fwlink/?linkID=227685).|  
|Bases de datos e instancias de PowerPivot para SharePoint|Compatibilidad limitada. Puede utilizar las conexiones HTTP y el proveedor SQLAS para ver información de las bases de datos y las instancias.<br /><br /> Sin embargo, no se admite el uso de los cmdlets. No debe utilizar Analysis Services PowerShell para las copias de seguridad y restauración de bases de datos PowerPivot en memoria, ni debe agregar o quitar roles, procesar datos o ejecutar script XMLA arbitrario.<br /><br /> Para la configuración, PowerPivot para SharePoint tiene una compatibilidad integrada con PowerShell que se proporciona por separado. Para obtener más información, consulte [referencia de PowerShell para PowerPivot para SharePoint](/sql/analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint).|  
|Conexiones nativas a cubos locales<br /><br /> "Datos Source=c:\backup\test.cub"|No compatible.|  
|Conexiones HTTP a archivos de conexión de modelos semánticos BI (.bism) en SharePoint<br /><br /> "Origen de datos =http://server/shared_docs/name.bism"|No compatible.|  
|Conexiones incrustadas a bases de datos PowerPivot<br /><br /> "Origen de datos = $Embedded$"|No compatible.|  
|Contexto del servidor local en los procedimientos almacenados de Analysis Services<br /><br /> "Origen de datos = *"|No compatible.|  
  
##  <a name="bkmk_auth"></a> Requisitos de autenticación y consideraciones de seguridad  
 Al conectarse a Analysis Services, debe realizar la conexión utilizando una identidad de usuario de Windows. En su mayor parte, una conexión se realiza utilizando la seguridad integrada de Windows, donde la identidad del usuario actual establece el contexto de seguridad en el que se realizan las operaciones de servidor. Sin embargo, están disponibles métodos de autenticación adicionales cuando se configura el acceso a Analysis Services a través de HTTP. En esta sección se explica cómo el tipo de conexión determina qué opciones de autenticación se pueden usar.  
  
 Las conexiones a Analysis Services se caracterizan como conexiones nativas o conexiones HTTP. Una conexión nativa es una conexión directa de una aplicación cliente con el servidor. En una sesión de PowerShell, el cliente de PowerShell utiliza el proveedor OLE DB para la conexión directa de Analysis Services con una instancia de Analysis Services. Una conexión nativa se realiza siempre utilizando la seguridad integrada de Windows, donde Analysis Services PowerShell se ejecuta como el usuario actual. Analysis Services no admite la suplantación. Si desea realizar una operación como un usuario específico, debe iniciar la sesión de PowerShell como ese usuario.  
  
 Las conexiones HTTP se realizan indirectamente a través de IIS, permitiendo opciones adicionales de autenticación, como la autenticación básica, para conectarse a una instancia de Analysis Services. Como IIS admite la suplantación, se puede proporcionar una cadena de conexión que incluya credenciales que IIS utilizará para realizar la suplantación cuando se realice una conexión. Para proporcionar las credenciales, puede usar el parámetro - Credential.  
  
 **Mediante el parámetro - Credential en PowerShell**  
  
 -Credential parámetro toma un objeto PSCredential que especifica un nombre de usuario y una contraseña. En Analysis Services PowerShell,-Credential parámetro está disponible para los cmdlets que realizan una solicitud de conexión a Analysis Services, en lugar de los cmdlets que se ejecutan dentro del contexto de una conexión existente. Entre los cmdlets que realizan una solicitud de conexión se hallan Invoke-ASCmd, Backup-ASDatabase y Restore-ASDatabase. Para estos cmdlets,-Credential parámetro puede usarse, suponiendo que se cumplen los criterios siguientes:  
  
1.  El servidor se configura para el acceso a través de HTTP, lo que significa que IIS administra la conexión, lee el nombre de usuario y la contraseña, y suplanta la identidad del usuario al conectarse a Analysis Services. Para obtener más información, vea [Configurar el acceso HTTP a Analysis Services en Internet Information Services &#40;IIS&#41; 8.0](instances/configure-http-access-to-analysis-services-on-iis-8-0.md).  
  
2.  El directorio virtual de IIS creado para el acceso a Analysis Services a través de HTTP se configura para la autenticación básica.  
  
3.  El nombre de usuario y la contraseña proporcionados por el objeto de credencial se resuelve como una identidad de usuario de Windows. Analysis Services utiliza esta identidad como usuario actual. Si el usuario no es un usuario de Windows, o carece de los permisos suficientes para realizar la operación solicitada, la solicitud dará un error.  
  
 Para crear un objeto de credencial, puede utilizar el cmdlet Get-Credential para recopilar las credenciales del operador. A continuación, puede utilizar el objeto de credencial en un comando que realiza la conexión a Analysis Services. En el ejemplo siguiente se muestra un enfoque. En este ejemplo, la conexión se realiza a una instancia local configurada para el acceso a través de HTTP.  
  
```  
PS SQLSERVER:\SQLAS\HTTP_DS> $cred = Get-credential adventureworks\dbadmin  
PS SQLSERVER:\SQLAS\HTTP_DS> Invoke-ASCmd -Inputfile:"c:\discoverconnections.xmla" -Credential:$cred  
```  
  
 Cuando se utiliza la autenticación básica, debe utilizar siempre HTTPS con SSL para que el nombre de usuario y las contraseñas se envíen mediante una conexión cifrada. Para obtener más información, consulte [configurar capa de Sockets seguros en IIS 7.0](https://go.microsoft.com/fwlink/?linkID=184299) y [configurar la autenticación básica (IIS 7)](https://go.microsoft.com/fwlink/?LinkId=230776).  
  
 Recuerde que las credenciales, las consultas, y los comandos que se proporcionan en PowerShell se pasan sin cambiar a la capa de transporte. La inclusión de contenido confidencial en los scripts aumenta el riesgo de un ataque malintencionado por inyección.  
  
 **Proporcionar una contraseña como un objeto Microsoft.Secure.String**  
  
 Algunas operaciones, como copias de seguridad y restauración, admiten opciones de cifrado que se activan al proporcionar una contraseña en el comando. La acción de proporcionar la contraseña indica a Analysis Services que se ha de cifrar o descifrar el archivo de copia de seguridad. En Analysis Services, se crea una instancia de esta contraseña como un objeto de cadena seguro. En el ejemplo siguiente se proporciona una ilustración de cómo se recopila una contraseña del operador en tiempo de ejecución.  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default> $pwd = read-host -AsSecureString -Prompt "Password"  
Password: ****  
PS SQLSERVER:\SQLAS\Localhost\default> $pwd -is [System.IDisposable]   
True  
```  
  
 Ahora puede realizar una operación de copia de seguridad o de restauración en un archivo de base de datos cifrado pasando la variable $pwd al parámetro de contraseña. Para ver un ejemplo completo que combina esta ilustración con otros cmdlets, consulte [cmdlet Backup-ASDatabase](/sql/analysis-services/powershell/backup-asdatabase-cmdlet) y [cmdlet Restore-ASDatabase](/sql/analysis-services/powershell/restore-asdatabase-cmdlet).
  
 Como paso de seguimiento, quite de la sesión tanto la contraseña como la variable.  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default> $pwd.Dispose()  
PS SQLSERVER:\SQLAS\Localhost\default> Remove-Variable -Name pwd  
```  
  
##  <a name="bkmk_tasks"></a> Tareas de PowerShell de Analysis Services  
 Puede ejecutar Analysis Services PowerShell desde el shell de administración de Windows PowerShell o desde un símbolo del sistema de Windows. No se admite la ejecución de Analysis Services PowerShell desde [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
 En esta sección se describen las tareas comunes para utilizar Analysis Services PowerShell.  
  
-   [El análisis de carga de servicios de proveedor y los Cmdlets](#bkmk_load)  
  
-   [Habilitar la administración remota](#bkmk_remote)  
  
-   [Conectarse a un análisis de servicios de objeto](#bkmk_connect)  
  
-   [Administrar el servicio](#bkmk_admin)  
  
-   [Obtener ayuda para Analysis Services PowerShell](#bkmk_help)  
  
###  <a name="bkmk_load"></a> El análisis de carga de servicios de proveedor y los Cmdlets  
 El proveedor de Analysis Services es una extensión del proveedor raíz de SQL Server que está disponible al importar el módulo SQLPS. Los cmdlets de Analysis Services se cargan simultáneamente; también puede cargarlos de modo independiente si desea utilizarlos con el proveedor.  
  
-   Ejecute el cmdlet del módulo Import para cargar el SQLPS que incluye toda la funcionalidad de Analysis Services PowerShell. Si no puede importar el módulo, puede cambiar temporalmente la directiva de ejecución a unrestricted con el fin de cargar el módulo. Para más información, vea [Importar el módulo SQLPS](../../2014/database-engine/import-the-sqlps-module.md).  
  
    ```  
    Import-module "sqlps"  
    ```  
  
     O bien, use `import-module "sqlps" -disablenamechecking` para quitar la advertencia sobre los nombres de verbo no aprobados.  
  
-   Para cargar solo los cmdlets de Analysis Services específicos de la tarea, sin el proveedor de Analysis Services o el cmdlet Invoke-ASCmd, puede cargar el módulo SQLASCmdlets como una operación independiente.  
  
    ```  
    Import-module "sqlascmdlets"  
    ```  
  
###  <a name="bkmk_remote"></a> Habilitar la administración remota  
 Para poder utilizar Analysis Services PowerShell con una instancia remota de Analysis Services, primero debe habilitar la administración remota y el uso compartido de archivos. El siguiente error indica un problema de configuración de firewall: "El servidor de RPC no está disponible. (Excepción de HRESULT: 0x800706BA)".  
  
1.  Compruebe que el equipo local y los equipos remotos tienen las versiones de [!INCLUDE[ssASCurrent](../includes/ssascurrent-md.md)] de las herramientas de servidor y de cliente.  
  
2.  En el servidor remoto que hospeda una instancia de Analysis Services, abra el puerto TCP 2383 en Firewall de Windows. Si instaló Analysis Services como una instancia con nombre o con un puerto personalizado, el número de puerto será diferente. Para obtener más información, consulte [Configure the Windows Firewall to Allow Analysis Services Access](instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
3.  En el servidor remoto, compruebe que se han iniciado los siguientes servicios:  Servicio remoto de llamada a procedimiento (RPC), servicio auxiliar de NetBIOS de TCP/IP, el servicio de Windows Management Instrumentation (WMI), el servicio Administración remota de Windows (WS-Management).  
  
4.  En el servidor remoto, inicie el complemento Editor de objetos de directiva de grupo (gpedit.msc).  
  
5.  Abra sucesivamente Configuración del equipo, Plantillas administrativas, Red, Conexiones de red,Firewall de Windows y, por último, Perfil de dominio.  
  
6.  Haga doble clic en **Firewall de Windows: Permitir excepción de administración remota entrante**, seleccione **habilitado**y, a continuación, haga clic en **Aceptar**.  
  
7.  Haga doble clic en **Firewall de Windows: Permitir excepción compartir impresoras y archivos de entrada**, seleccione **habilitado**y, a continuación, haga clic en **Aceptar**.  
  
8.  En el equipo local que tiene las herramientas de cliente, use los siguientes cmdlets para comprobar la administración remota, sustituyendo el nombre de servidor real por el *nombre del servidor remoto* marcador de posición. Omita el nombre de instancia si Analysis Services se instala como la instancia predeterminada. Debe haber importado previamente el módulo SQLPS para que el comando funcione.  
  
    ```  
    PS SQLSERVER:\> cd sqlas  
    PS SQLSERVER:\sqlas> cd <remote-server-name\instance-name>  
    PS SQLSERVER:\sqlas\<remote-server-name\instance-name> dir  
    ```  
  
 En algunos casos, es posible que sea necesaria una configuración adicional. Puede que tenga que escribir lo siguiente en el servidor remoto para poderle emitir comandos desde otro equipo:  
  
```  
Enable-psremoting  
```  
  
  
###  <a name="bkmk_connect"></a> Conectarse a un análisis de servicios de objeto  
 El proveedor de Analysis Services PowerShell admite la navegación de la jerarquía de objetos de Analysis Services y establece el contexto para los comandos en ejecución. El proveedor es una extensión del proveedor raíz de SQLSERVER disponible a través del módulo SQLPS. Después de cargar el módulo SQLPS, puede navegar por la ruta de acceso.  
  
 Puede conectarse a una instancia local o remota, pero algunos cmdlets solo se pueden ejecutar en una instancia local (a saber, merge-partition). Puede utilizar una conexión nativa o una conexión HTTP para los servidores de Analysis Services que configuró para el acceso HTTP. En las ilustraciones siguientes se muestra la ruta de acceso de navegación de las conexiones HTTP y nativas. En las ilustraciones siguientes se muestra la ruta de acceso de navegación de las conexiones HTTP y nativas.  
  
 **Conexiones nativas a Analysis Services**  
  
 ![Conexión nativa a Analysis Services](media/ssas-powershell-nativeconnection.gif "conexión nativa a Analysis Services")  
  
 El ejemplo siguiente es una demostración de cómo utilizar una conexión nativa para navegar por la jerarquía de objetos. Desde el proveedor, puede emitir un `dir` para ver la información de la instancia. Puede utilizar `cd` para ver los objetos de esa instancia.  
  
```  
PS SQLSERVER:> cd sqlas  
PS SQLSERVER\sqlas:> dir  
PS SQLSERVER\sqlas:> cd localhost\default  
PS SQLSERVER\sqlas\localhost\default:> dir  
```  
  
 Debería ver las siguientes colecciones: Los ensamblados, las bases de datos, Roles y seguimientos. Si continúa utilizando `cd` y `dir`, puede ver el contenido de cada colección.  
  
 **Conexiones HTTP a Analysis Services**  
  
 ![Conexión de HTTP a Analysis Services](media/ssas-powershell-httpconnection.gif "conexión HTTP a Analysis Services")  
  
 Las conexiones HTTP son útiles si ha configurado el servidor para el acceso HTTP con las instrucciones de este tema: [Configurar el acceso HTTP a Analysis Services en Internet Information Services &#40;IIS&#41; 8.0](instances/configure-http-access-to-analysis-services-on-iis-8-0.md)  
  
 Suponiendo que una dirección URL del servidor de http://localhost/olap/msmdpump.dll, una conexión podría ser similar al siguiente:  
  
```  
PS SQLSERVER\sqlas:> cd http_ds  
PS SQLSERVER\sqlas\http_ds:> $Url=Encode-SqlName "http://localhost/olap/msmdpump.dll"  
PS SQLSERVER\sqlas\http_ds:> cd $Url  
PS SQLSERVER\sqlas\http_ds\http%3A%2F%2Flocalhost%2olap%2msmdpump%2Edll:> dir  
```  
  
 Debería ver las siguientes colecciones: Los ensamblados, las bases de datos, Roles y seguimientos. Si no puede ver el contenido de estas colecciones, compruebe la configuración de la autenticación en el directorio virtual OLAP. Asegúrese de que el acceso anónimo está deshabilitado. Si utiliza la autenticación de Windows, asegúrese de que la cuenta de usuario de Windows tiene permisos administrativos en la instancia de Analysis Services.  
  
###  <a name="bkmk_admin"></a> Administrar el servicio  
 Compruebe que el servicio se está ejecutando. Devuelve el estado, el nombre y el nombre para mostrar de servicios de SQL Server, incluido Analysis Services (MSSQLServerOLAPService) y el motor de base de datos.  
  
```  
Get-service mssql*  
```  
  
 Devuelve las propiedades de un proceso, incluido el identificador de proceso, el recuento de identificadores y el uso de memoria:  
  
```  
Get-process msmdsrv  
```  
  
 Reinicia el servicio al emitir el cmdlet siguiente desde el shell de administración:  
  
```  
Restart-service mssqlserverolapservice  
```  
  
###  <a name="bkmk_help"></a> Obtener ayuda para Analysis Services PowerShell  
 Use cualquiera de los siguientes cmdlets para comprobar su disponibilidad y obtener más información acerca de los servicios, los procesos y los objetos.  
  
1.  `Get-help` devuelve la Ayuda integrada para un cmdlet de Analysis Services, incluidos los ejemplos:  
  
    ```  
    Get-help invoke-ascmd -examples  
    ```  
  
2.  `Get-command` devuelve una lista de los once cmdlets de Analysis Services PowerShell:  
  
    ```  
    get-command -module SQLASCmdlets  
    ```  
  
3.  `Get-member` devuelve las propiedades o los métodos de un servicio o un proceso.  
  
    ```  
    Get-service mssqlserverolapservice | get-member -type Property  
    ```  
  
    ```  
    Get-service mssqlserverolapservice | get-member -type Method  
    ```  
  
    ```  
    Get-process msmdsrv | get-member -type Property  
    ```  
  
4.  `Get-member` también se puede utilizar para devolver las propiedades o los métodos de un objeto (por ejemplo, los métodos AMO en el objeto de servidor) mediante el proveedor SQLAS para especificar la instancia de servidor.  
  
    ```  
    PS SQLSERVER:\sqlas\localhost\default > $serverObj = New-Object Microsoft.AnalysisServices.Server  
    PS SQLSERVER:\sqlas\localhost\default > $serverObj = | get-member -type Method  
    ```  
  
5.  `Get-PSdrive` devuelve una lista de los proveedores instalados actualmente. Si importó el módulo SQLPS, verá el proveedor `SQLServer` en la lista (SQLAS forma parte del proveedor SQLServer y nunca aparece de forma independiente en la lista):  
  
    ```  
    Get-PSDrive  
    ```  
  
## <a name="see-also"></a>Vea también  
 [Instalar SQL Server PowerShell](../database-engine/install-windows/install-sql-server-powershell.md)   
 [Administrar modelos tabulares con PowerShell (blog)](https://go.microsoft.com/fwlink/?linkID=227685)   
 [Configurar el acceso HTTP a Analysis Services en Internet Information Services &#40;IIS&#41; 8.0](instances/configure-http-access-to-analysis-services-on-iis-8-0.md)  
  
  
