---
title: "PowerShell scripting in Analysis Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 60bb9610-7229-42eb-a95f-a377268a8720
caps.latest.revision: 44
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 44
---
# PowerShell scripting in Analysis Services
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] incorpora componentes de PowerShell para navegar por objetos multidimensionales, tabulares y de servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], así como para administrarlos y realizar consultas en ellos:  
  
-   El proveedor **SQLAS**, que se usa para navegar por la jerarquía de objetos, está disponible cuando se tiene una instancia local de Analysis Services (el modo de servidor es irrelevante).  
  
-   El módulo **SQLASCMDLETS** proporciona cmdlets específicos de tareas, como copia de seguridad, restauración y procesamiento, así como el [cmdlet Invoke-ASCmd](../../analysis-services/powershell/invoke-ascmd-cmdlet.md) de uso general, que acepta cualquier archivo de entrada de script o consulta ASSL/XMLA o Tabular Model Scripting Language (TMSL).  
  
 Estos componentes implementan un subconjunto de la interfaz administrativa de Objeto de administración de Analysis Services ([Microsoft.AnalysisServices Namespace](http://msdn.microsoft.com/library/ms146720\(SQL.130\).aspx)) y ofrecen cmdlets para administrar y crear objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  Ambos son extensiones del módulo raíz **SQLPS** para SQL Server. Para usar componentes de PowerShell de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], debe empezar importando **SQLPS**. Podrá encontrar la sintaxis y ejemplos de todos los cmdlets en [Analysis Services PowerShell Reference](../../analysis-services/powershell/analysis-services-powershell-reference.md).  Para obtener un ejemplo de cómo utilizar los tipos AMO en PowerShell para crear una base de datos tabular, consulte [AMO PowerShell Example](../../analysis-services/powershell/amo-powershell-example.md).  
  
##  <a name="bkmk_prereq"></a> Paso 1: instalación de los componentes de PowerShell  
 Para obtener los componentes de PowerShell, se recomienda instalar SQL Server Management Studio (SSMS). Así se podrán conseguir los módulos de PowerShell para SQL Server y el proveedor de datos de administración de Analysis Services (AMO). Con SSMS también contará con una herramienta para generar fácilmente XMLA y entradas TMSL que podrá utilizar en el script de PowerShell.  
  
 Considere la posibilidad de instalar una instancia local de Analysis Services. Una instancia local permite la navegación por la jerarquía de objetos a través del proveedor **SQLAS** , incluso si nunca se utiliza para hospedar una base de datos.  
  
1.  Vaya a  [Download SQL Server Management Studio](https://msdn.microsoft.com/en-us/library/mt238290.aspx) (Descargar SQL Server Management Studio [SSMS]) para conseguir la versión más reciente de Management Studio. La versión más reciente de Management Studio incluye un AMO actualizado que admite las definiciones de objeto de metadatos tabulares, orientadas a los modelos tabulares creados con el nivel de compatibilidad 1200.  
  
2.  Después de instalar Management Studio, abra una ventana de PowerShell. No tiene que ser una ventana de administrador.  
  
3.  Escriba `Get-Module -ListAvailable` para confirmar que los módulos **SQLPS** y **SQLASCMDLETS** figuran en la lista.  
  
     No verá **SQLAS** a menos que también instale una instancia local de Analysis Services (modo tabular o multidimensional).  
  
4.  Escriba `Get-Command -Module sqlascmdlets` para generar una lista de los cmdlets usados en la administración de Analysis Services.  
  
     **SQLASCMDLETS** están disponibles incluso cuando falte el proveedor **SQLAS** .  
  
    -   [Cmdlet Add-RoleMember](../../analysis-services/powershell/add-rolemember-cmdlet.md)  
  
    -   [Cmdlet Backup-ASDatabase](../../analysis-services/powershell/backup-asdatabase-cmdlet.md)  
  
    -   [Cmdlet Invoke-ASCmd](../../analysis-services/powershell/invoke-ascmd-cmdlet.md) **-inputfile**  
  
    -   [Invoke-ProcessASDatabase](../../analysis-services/powershell/invoke-processasdatabase.md)  
  
    -   [Cmdlet Invoke-ProcessCube](../../analysis-services/powershell/invoke-processcube-cmdlet.md)  
  
    -   [Cmdlet Invoke-ProcessDimension](../../analysis-services/powershell/invoke-processdimension-cmdlet.md)  
  
    -   [Cmdlet Invoke-ProcessPartition](../../analysis-services/powershell/invoke-processpartition-cmdlet.md)  
  
    -   [Cmdlet Invoke-ProcessTable](../../analysis-services/powershell/invoke-processtable-cmdlet.md)  
  
    -   [Cmdlet Merge-Partition](../../analysis-services/powershell/merge-partition-cmdlet.md)  
  
    -   [Cmdlet New-RestoreFolder](../../analysis-services/powershell/new-restorefolder-cmdlet.md)  
  
    -   [Cmdlet New-RestoreLocation](../../analysis-services/powershell/new-restorelocation-cmdlet.md)  
  
    -   [Cmdlet Remove-RoleMember](../../analysis-services/powershell/remove-rolemember-cmdlet.md)  
  
    -   [Cmdlet Restore-ASDatabase](../../analysis-services/powershell/restore-asdatabase-cmdlet.md)  
  
> [!NOTE]  
>  Windows PowerShell está instalado de manera predeterminada en las versiones más recientes de los sistemas operativos Windows. La recomendación es 4.0 o posterior.  
  
## Paso 2: carga de componentes para iniciar una sesión interactiva  
 Una vez instalados los componentes, al cargarlos se inicia una sesión interactiva.  
  
1.  Escriba `Import-Module sqlps -DisableNameChecking`.  
  
     Carga los componentes de SQL Server PowerShell, incluidos los de Analysis Services, y suprime la advertencia sobre los nombres de verbo no válidos.  
  
2.  Escriba `sqlserver:`  
  
     Debería ver que el símbolo del sistema cambia a **PS SQLSERVER:\\>**.  
  
3.  Si Analysis Services está instalado localmente, puede navegar por la jerarquía de objetos. Escriba `cd sqlas` para abrir el proveedor **SQLAS**.  
  
4.  Escriba `dir` para enumerar las instancias de Analysis Services. El proveedor no distingue entre las instancias tabulares y multidimensionales.  
  
## Permissions  
 Una sesión interactiva de PowerShell se ejecuta con la identidad de seguridad de la persona que la inicie. La mayoría de las tareas requerirán que la persona que inicia la sea también administrador del servidor de Analysis Services.  
  
 Las tareas programadas de PowerShell deben considerarse operaciones desatendidas. También es muy probable que la cuenta con la que se ejecute el programador, como el servicio Agente SQL Server, deba ser de administrador de Analysis Services (en función de la tarea).  
  
 Las carpetas de datos locales, como los directorios predeterminados de datos y copia de seguridad, ya están configuradas con los permisos del sistema de archivos que permiten a una instancia local leer estas ubicaciones y escribir en ellas.  
  
 La administración remota, especialmente cuando se realiza desde equipos cliente que no tienen instalado Analysis Services, requiere que la instancia remota del servidor de Analysis Services que lleve a cabo la acción tenga permisos del sistema de archivos para leer archivos durante la restauración, o bien escribirlos durante la copia de seguridad.  
  
## Archivos de entrada de script: ASSL/XMLA o TMSL  
 Si usa **invoke-ascmd** para ejecutar un script, el modo de servidor, el tipo de base de datos y el nivel de compatibilidad repercutirán en cómo se debe crear el script.  
  
-   Las bases de datos multidimensionales y tabulares con niveles de compatibilidad 1050 y 1103 responden a scripts escritos en XMLA (con las extensiones ASSL específicas de las definiciones de objetos de Analysis Services).  
  
-   Por su parte, las bases de datos tabulares de SQL Server 2016 (nivel de compatibilidad 1200) responden a los scripts elaborados con TMSL.  
  
 Si está trabajando con versiones mixtas de modelos tabulares en la misma instancia de SQL Server 2016, recuerde que debe usar el script correcta.  
  
> [!NOTE]  
>  Es posible generar los scripts en SQL Server Management Studio y, después, modificarlos según sea necesario. Los scripts para bases de datos tabulares con el nivel de compatibilidad 1200 se crean en TMSL. Todos los demás se programan con XMLA y ASSL. Una instancia de SQL Server 2016 en modo tabular admite ambos lenguajes de scripting.  
  
## Administración remota y local  
 La administración local de Analysis Services mediante scripts y comandos de PowerShell resulta más sencilla por dos motivos:  
  
-   Permite utilizar el proveedor **SQLAS** para navegar por la jerarquía de objetos.  
  
-   Los permisos de archivo que permiten a Analysis Services leer las carpetas de datos predeterminadas, como en el caso de las tareas de copia de seguridad y restauración, ya se han otorgado, suponiendo que utilice dichas carpetas como la ubicación de la base de datos y se use la instancia del servidor local para la operación.  
  
 Para administrar una instancia remota, se precisa una mayor configuración. En los siguientes pasos se asume que ha completado los pasos de instalación de Management Studio, pero que la instancia de servicio se encuentra en un equipo remoto. Debe contar con derechos de administrador en el servidor de Analysis Services.  
  
 Como Analysis Services se encuentra en un equipo remoto, no hay ningún proveedor **SQLAS** navegar localmente por la jerarquía de objetos. Si pretende restaurar archivos desde una carpeta local en lugar de una instancia de Analysis Services, tendrá que crear recursos compartidos y otorgar al servidor acceso de lectura a los archivos.  
  
1.  Abra una ventana de administrador de PowerShell.  
  
2.  Escriba `Set-ExecutionPolicy RemoteUnsigned`  
  
3.  En el Explorador de archivos, asegúrese de que se hayan compartido todas las carpetas que almacenan archivos de datos y que la instancia de Analysis Services dispone de permisos de lectura para el contenido.  
  
##  <a name="bkmk_vers"></a> Versiones admitidas y modos de Analysis Services  
 En la tabla siguiente es muestra la disponibilidad de Analysis Services PowerShell en varios contextos.  
  
|Contexto|Disponibilidad de las características de PowerShell|  
|-------------|-------------------------------------|  
|Bases de datos e instancias multidimensionales|Se admite para la administración remota y local.<br /><br /> Merge-partition requiere una conexión local.|  
|Bases de datos e instancias tabulares|Se admite para la administración remota y local, con todos los niveles de compatibilidad.<br /><br /> Cmdlets de SQLAS para los modelos tabulares con el nivel de compatibilidad 1200 mediante el uso de Tabular Model Scripting Language (TMSL) en JSON en lugar de XMLA.|  
|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint|Compatibilidad limitada. Puede utilizar las conexiones HTTP y el proveedor SQLAS para ver información de las bases de datos y las instancias.<br /><br /> Sin embargo, no se admite el uso de los cmdlets. No puede usar PowerShell de Analysis Services para realizar copias de seguridad de una base de datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en memoria o restaurarla, ni debe agregar o quitar roles, procesar información o ejecutar scripts XMLA arbitrarios.<br /><br /> En lo que respecta a la configuración, [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint tiene una compatibilidad integrada con PowerShell que se proporciona por separado. Para obtener más información, vea [Referencia de PowerShell para Power Pivot para SharePoint](../../analysis-services/powershell/powershell-reference-for-power-pivot-for-sharepoint.md).|  
|Conexiones nativas a cubos locales<br /><br /> “Data Source=c:\backup\test.cub”|No compatible.|  
|Conexiones HTTP a archivos de conexión de modelos semánticos BI (.bism) en SharePoint<br /><br /> “Data Source=http://server/shared_docs/name.bism”|No compatible.|  
|Conexiones incrustadas a bases de datos [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]<br /><br /> “Data Source=$Embedded$”|No compatible.|  
|Contexto del servidor local en los procedimientos almacenados de Analysis Services<br /><br /> “Data Source=*”|No compatible.|  
  
## Ejemplos de tareas de administración del servidor con PowerShell  
 **Enumerar las propiedades del servidor**  
  
 Las propiedades del servidor se exponen de varias formas.  Si está familiarizado con las propiedades expuestas en msmdsrv. ini o en las páginas de propiedades de Management Studio, podrá ver en los ejemplos siguientes que realmente se devuelven propiedades de objetos distintos.  
  
 Este script carga un objeto de servidor de AMO. Si necesita un nombre de propiedad completo, puede ejecutar este script para obtener la lista.  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as.connect("server-name\instance-name")  
$as.serverproperties  
  
```  
  
 Este script devuelve propiedades y métodos de nivel de instancia. En esta lista, puede leer valores como **ServerMode**, **Version**, **ProductName**o **ProductLevel**.  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as | get-member  
  
```  
  
 **Obtener el modo de servidor**  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as.ServerMode  
```  
  
 **Obtener el nivel de compatibilidad predeterminado**  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as.DefaultCompatibilityLevel  
```  
  
 **Obtener una lista de bases de datos**  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as.databases  
```  
  
 **Cambiar el número de puerto**  
  
 Este script crea un objeto para una instancia con nombre, declara y establece el puerto, actualiza la instancia de servidor, desconecta el objeto, y reinicia el servicio. Como paso de verificación, puede iniciar una nueva conexión y devolver el puerto.  
  
 También tiene la posibilidad de comprobar el puerto en el archivo msmdsrv.ini o en la página de propiedades General del servidor en Management Studio.  
  
```  
sqlps  
$as = New-Object Microsoft.AnalysisServices.Server  
$as.connect("server-name\instance-name")  
$port = $as.serverproperties['Port']  
$port | select *  
$port.Value = [int]55555  
$as.Update()  
$as.Disconnect()  
restart-service 'MSOLAP$TABULAR'  
$as.connect("server-name\instance-name")  
$port | select *  
  
```  
  
## Vea también  
 [Conceder permisos de administrador de servidor (Analysis Services)](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)   
 [Nivel de compatibilidad para modelos tabulares de Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Tabular Model Scripting Language &#40;TMSL&#41; Reference (Referencia de Tabular Model Scripting Language [TMSL])](../Topic/Tabular%20Model%20Scripting%20Language%20\(TMSL\)%20Reference.md)   
 [Instalar SQL Server PowerShell](../../database-engine/install-windows/install-sql-server-powershell.md)   
 [Administrar modelos tabulares con PowerShell](http://go.microsoft.com/fwlink/?linkID=227685)   
 [Configurar el acceso HTTP a Analysis Services en Internet Information Services &#40;IIS&#41; 8.0](../../analysis-services/instances/configure http access to analysis services on iis 8.0.md)  
  
  