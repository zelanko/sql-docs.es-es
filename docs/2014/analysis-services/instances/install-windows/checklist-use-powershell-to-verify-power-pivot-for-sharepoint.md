---
title: 'Lista de comprobación: Use PowerShell para comprobar PowerPivot para SharePoint | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 73a13f05-3450-411f-95f9-4b6167cc7607
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 868fb0f7176faf1c1e795b8efe43f8b6d4cdb3f5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "76918098"
---
# <a name="checklist-use-powershell-to-verify-powerpivot-for-sharepoint"></a>Lista de comprobación: Usar PowerShell para comprobar PowerPivot para SharePoint
  Ninguna operación de instalación o recuperación de [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] está completa sin un paso sólido de comprobación que confirme que los servicios y los datos son operativos. En este artículo, le mostramos cómo realizar estos pasos con Windows PowerShell. Cada paso tiene su propia sección para que pueda ir directamente a determinadas tareas. Por ejemplo, ejecute el script de la sección [Bases de datos](#bkmk_databases) de este tema para comprobar el nombre de la aplicación de servicio y las bases de datos de contenido si desea programar su mantenimiento o copia de seguridad.  
  
|||  
|-|-|  
|![Contenido relacionado con PowerShell](../../../reporting-services/media/rs-powershellicon.jpg "Contenido relacionado con PowerShell")|Al final del tema se incluye un script completo de PowerShell. Use el script completo como punto de partida para generar un script personalizado con el fin de auditar toda la implementación de [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)].|  
  
||  
|-|  
|**[!INCLUDE[applies](../../../includes/applies-md.md)]** SharePoint 2013 &#124; SharePoint 2010|  
  
 **En este tema**: los elementos con letras de la tabla de contenido siguiente corresponden a las áreas del diagrama. El diagrama muestra  
  
|||  
|-|-|  
|[Preparar el entorno de PowerShell](#bkmk_prerequisites)<br /><br /> [Síntomas y acciones recomendadas](#bkmk_symptoms)<br /><br /> **(A)** [Analysis Services servicio de Windows](#bkmk_windows_service)<br /><br /> **(B)** [PowerPivotSystemService y PowerPivotEngineService](#bkmk_engine_and_system_service)<br /><br /> **(C)** [aplicaciones de servicio PowerPivot y servidores proxy](#bkmk_powerpivot_service_application)<br /><br /> **(D)** [bases de datos](#bkmk_databases)<br /><br /> [Características de SharePoint](#bkmk_features)<br /><br /> [Trabajos de temporizador](#bkmk_timer_jobs)<br /><br /> [Reglas de estado](#bkmk_health_rules)<br /><br /> **(E)** [registros de Windows y ULS](#bkmk_logs)<br /><br /> [Proveedor MSOLAP](#bkmk_msolap)<br /><br /> [Biblioteca de cliente de ADOMD.Net](#bkmk_adomd)<br /><br /> [Reglas de recopilación de datos de mantenimiento](#bkmk_health_collection)<br /><br /> [Soluciones](#bkmk_solutions)<br /><br /> [Pasos de comprobación manual](#bkmk_manual)<br /><br /> [Más recursos](#bkmk_more_resources)<br /><br /> [Script completo de PowerShell](#bkmk_full_script)|![comprobación de powershell de powerpivot](../../../sql-server/install/media/ssas-powershell-component-verification.png "comprobación de powershell de powerpivot")|  
  
##  <a name="bkmk_prerequisites"></a>Preparar el entorno de PowerShell  
 Los pasos de esta sección sirven para preparar el entorno de PowerShell. Puede que estos pasos no sean necesarios, en función de cómo esté configurado actualmente el entorno de scripting.  
  
 **Permisos de PowerShell**  
  
 Abra una ventana de Powershell o ISE (Entorno de scripting integrado) de PowerShell con **privilegios administrativos**. Si no tiene privilegios administrativos al ejecutar comandos, verá un mensaje de error similar al siguiente:  
  
 Get-SPLogEvent: Debe tener **privilegios de administrador** del equipo para ejecutar este cmdlet.  
  
 **SharePoint y [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] ** Destina  
  
 Si ve un mensaje de error similar al siguiente al ejecutar cmdlets relacionados de SharePoint, ejecute el comando Add-PSSnapin:  
  
 El término 'Get-PowerPivotSystemService' **no se reconoce como nombre de un cmdlet**, función, archivo de script o programa ejecutable. Compruebe si escribió correctamente el nombre o, si incluyó una ruta de acceso, compruebe que dicha ruta es correcta e inténtelo de nuevo.  
  
```  
Add-PSSnapin Microsoft.Sharepoint.Powershell -EA 0  
```  
  
 **Windows PowerShell**  
  
 Para obtener más información sobre el ISE de PowerShell, vea [Introducción a ISE de Windows PowerShell](https://technet.microsoft.com/library/dd315244.aspx) y [Usar Windows PowerShell para administrar SharePoint 2013](https://technet.microsoft.com/library/ee806878\(v=office.15\).aspx).  
  
|||  
|-|-|  
|![powerpivot en conjunto de aplicaciones general de sharepoint](../../../sql-server/install/media/ssas-powerpivot-logo.png "powerpivot en conjunto de aplicaciones general de sharepoint")|Si lo desea, puede comprobar la mayoría de los componentes en Administración central, con el panel de administración de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] . Para abrir el panel en Administración central, haga clic en **Configuración de aplicación general**y, a continuación, haga clic en **Panel de administración** en **PowerPivot**. Para obtener más información sobre el panel, vea [PowerPivot Management Dashboard and Usage Data](../../power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md).|  
  
##  <a name="bkmk_symptoms"></a>Síntomas y acciones recomendadas  
 En la tabla siguiente se muestra una lista de síntomas o problemas y la sección sugerida de este tema que puede consultar para resolver el problema.  
  
|Síntoma|Vea la sección|  
|-------------|-----------------|  
|La actualización de datos no está en ejecución|Vea la sección [Timer Jobs](#bkmk_timer_jobs) y compruebe que el **Trabajo de temporizador de actualización de datos de PowerPivot** está en línea.|  
|Los datos del panel de administración son antiguos|Vea la sección [Trabajos del temporizador](#bkmk_timer_jobs) y compruebe que el **Trabajo de temporizador de procesamiento del panel de administración** está en línea.|  
|Algunas partes del panel de administración|Si instala PowerPivot para SharePoint en una granja que tiene la topología de Administración central, sin Excel Services o PowerPivot para SharePoint, debe descargar e instalar la biblioteca de cliente de Microsoft ADOMD.NET si desea acceso total a los informes integrados en el panel de administración de PowerPivot. Algunos informes del panel usan ADOMD.NET para tener acceso a los datos internos que proporcionan los datos de errores en el procesamiento de las consultas de PowerPivot y el estado del servidor en la granja. Vea la sección [Biblioteca de cliente de ADOMD.NET](#bkmk_adomd) y el tema [Instalar ADOMD.NET en servidores front-end web ejecutando Administración central](../../../sql-server/install/install-adomd-net-on-web-front-end-servers-running-central-administration.md).|  
|\<> de contenido futuro||  
  
##  <a name="bkmk_windows_service"></a>Analysis Services servicio de Windows  
 El script de esta sección comprueba la instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] en modo de SharePoint. Compruebe que el servicio se está **ejecutando**.  
  
```powershell
Get-Service | Select name, displayname, status | Where {$_.Name -eq "msolap`$powerpivot"} | Format-Table -Property * -AutoSize | Out-Default  
```
  
```Output
Name              DisplayName                                Status  
----              -----------                                ------  
MSOLAP$POWERPIVOT SQL Server Analysis Services (POWERPIVOT) Running  
```  
  
##  <a name="bkmk_engine_and_system_service"></a>PowerPivotSystemService y PowerPivotEngineService  
 Los scripts de esta sección comprueban los servicios del sistema de [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] . Hay un servicio del sistema para una implementación de SharePoint 2013 y dos servicios para una implementación de SharePoint 2010.  
  
 **PowerPivotSystemService**  
  
 Compruebe que el estado es **en línea**.  
  
```powershell
Get-PowerPivotSystemService | Select typename, status, applications, farm | Format-Table -Property * -AutoSize | Out-Default  
```
  
```Output
TypeName                                  Status Applications                             Farm  
--------                                  ------ ------------                             ----  
SQL Server PowerPivot Service Application Online {Default PowerPivot Service Application} SPFarm Name=SharePoint_Config_77d8ab0744a34e8aa27c806a2b8c760c  
```  
  
 **PowerPivotEngineService**  
  
> [!NOTE]  
>  **Omita este script si** está usando SharePoint 2013. PowerPivotEngineService no forma parte de una implementación de SharePoint 2013. Si ejecuta el cmdlet Get-PowerPivot**Engine**Service en SharePoint 2013, verá un mensaje de error similar al siguiente. Este mensaje de error aparece aunque haya ejecutado el comando Add-PSSnapin que se describe en la sección de requisitos previos de este tema.  
>   
>  El término 'Get-PowerPivotEngineService' no se reconoce como nombre de un cmdlet  
  
 En una implementación de SharePoint 2010, compruebe que el estado es **En línea**.  
  
```powershell
Get-PowerPivotEngineService | Select typename, status, name, instances, farm | Format-Table -Property * -AutoSize | Out-Default
```
  
```Output  
TypeName  : SQL Server Analysis Services  
Status    : Online  
Name      : MSOLAP$POWERPIVOT  
Instances : {POWERPIVOT}  
Farm      : SPFarm Name=SharePoint_Config  
```  
  
##  <a name="bkmk_powerpivot_service_application"></a>Aplicaciones de servicio PowerPivot y servidores proxy  
 Compruebe que el estado es **En línea**. La Aplicación de Servicios de Excel no usa una base de datos de aplicación de servicio y por tanto el cmdlet no devuelve un nombre de base de datos. Anote la base de datos usada por la aplicación de servicio de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] para que pueda comprobar que está en línea en la sección de base de datos más adelante en este tema.  
  
 **PowerPivot y aplicaciones de servicio de Excel**  
  
 En una implementación de SharePoint 2010, compruebe que el estado es **En línea**.  
  
```powershell
Get-PowerPivotServiceApplication | Select typename,name, status, unattendedaccount, applicationpool, farm, database  
Get-SPExcelServiceApplication | Select typename, DisplayName, status  
```
  
```Output  
TypeName          : PowerPivot Service Application  
Name              : PowerPivotServiceApplication1  
Status            : Online  
UnattendedAccount : PowerPivotUnattendedAccount  
ApplicationPool   : SPIisWebServiceApplicationPool Name=sqlbi_serviceapp  
Farm              : SPFarm Name=SharePoint_Config  
Database          : GeminiServiceDatabase Name=PowerPivotServiceApplication1_19648f3f2c944e27acdc6c20aab8487a  
  
TypeName    : Excel Services Application Web Service Application  
DisplayName : Excel Services Application  
Status      : Online  
```  
  
 **Grupo de aplicaciones de servicio**  
  
> [!NOTE]  
>  El ejemplo de código siguiente devuelve la propiedad applicationpool de la aplicación de servicio de [!INCLUDE[ssGeminiShort](../../../includes/ssgeminishort-md.md)] predeterminada. El nombre se analiza de la cadena y se usa para obtener el estado del objeto de grupo de aplicaciones.  
>   
>  Compruebe que el estado es **en línea**. Si el estado no es en línea o ve "error http" al examinar el [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] sitio, compruebe que las credenciales de identidad de los grupos de aplicaciones de IIS siguen siendo correctas. El nombre del grupo de aplicaciones de IIS es el valor de la propiedad ID devuelto por el comando Get-SPServiceApplicationPool.  
  
```powershell
$poolname = [string](Get-PowerPivotServiceApplication | Select -Property applicationpool)  
$position = $poolname.lastindexof("=")  
$poolname = $poolname.substring($position+1)  
$poolname = $poolname.substring(0,$poolname.length-1)

Get-SPServiceApplicationPool | Select name, status, processaccountname, id | Where {$_.Name -eq $poolname} | Format-Table -Property * -AutoSize | Out-Default  
```
  
```Output
Name                           Status ProcessAccountName Id  
----                           ------ ------------------ -------   
SharePoint Web Services System Online DOMAIN\account     89b50ec3-49e3-4de7-881a-2cec4b8b73ea  
```  
  
 ![Nota:](../../../reporting-services/media/rs-fyinote.png "note") El grupo de aplicaciones también se puede comprobar en la página Administración central administración de **aplicaciones de servicio**. Haga clic el nombre de la aplicación de servicio y, a continuación, haga clic en **Propiedades** en la cinta de opciones.  
  
 **Servidores proxy de aplicaciones de servicio de Excel y PowerPivot**  
  
 Compruebe que el estado es **en línea**.  
  
```powershell
Get-SPServiceApplicationProxy | Select typename, status, unattendedaccount, displayname | Where {$_.TypeName -Like "*powerpivot*" -Or $_.TypeName -Like "*excel services*"} | Format-Table -Property * -AutoSize | Out-Default  
```
  
```Output
TypeName                                                 Status UnattendedAccount           DisplayName  
--------                                                 ------ -----------------           -----------  
PowerPivot Service Application Proxy                     Online PowerPivotUnattendedAccount PowerPivotServiceApplication1  
Excel Services Application Web Service Application Proxy Online                             Excel Services Application  
```  
  
##  <a name="bkmk_databases"></a>Bases  
 El script siguiente devuelve el estado de las bases de datos de aplicación de servicio y todas las bases de datos de contenido. Compruebe que el estado es **En línea**.  
  
```powershell
Get-SPDatabase | Select name, status, server, typename | Where {$_.TypeName -eq "content database" -Or $_.TypeName -Like "*Gemini*"} | Format-Table -Property * -AutoSize | Out-Default  
```
  
```Output
Name                                                                       Status Server                  TypeName   
----                                                                       ------ ------                  --------   
DefaultPowerPivotServiceApplicationDB-38422181-2b68-4ab2-b2bb-9c00c39e5a5e Online SPServer Name=TESTSERVER Microsoft.AnalysisServices.SPAddin.GeminiServiceDatabase  
DefaultWebApplicationDB-f0db1a8e-4c22-408c-b9b9-153bd74b0312               Online TESTSERVER\POWERPIVOT    Content Database   
SharePoint_Admin_3cadf0b098bf49e0bb15abd487f5c684                          Online TESTSERVER\POWERPIVOT    Content Database  
```  
  
##  <a name="bkmk_features"></a>Características de SharePoint  
 Compruebe que las características de sitio, web y granja están en línea.  
  
```powershell
Get-SPFeature | Select displayname, status, scope, farm | Where {$_.displayName -Like "*powerpivot*"} | Format-Table -Property * -AutoSize | Out-Default  
```
  
```Output
DisplayName     Status Scope Farm                           
-----------     ------ ----- ----                           
PowerPivotSite  Online  Site SPFarm Name=SharePoint_Config  
PowerPivotAdmin Online   Web SPFarm Name=SharePoint_Config  
PowerPivot      Online  Farm SPFarm Name=SharePoint_Config  
```  
  
##  <a name="bkmk_timer_jobs"></a>Trabajos de temporizador  
 Compruebe que los trabajos del temporizador están **En línea**. El EngineService de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] no está instalado en SharePoint 2013, por lo que el script no mostrará los trabajos del temporizador de EngineService en una implementación de SharePoint 2013.  
  
```powershell
Get-SPTimerJob | Where {$_.service -Like "*power*" -Or $_.service -Like "*mid*"} | Select status, displayname, LastRunTime, service | Format-Table -Property * -AutoSize | Out-Default  
```
  
```Output
      Status DisplayName                                                                          LastRunTime          Service                               
------ -----------                                                                          -----------          -------                               
Online Health Analysis Job (Daily, SQL Server Analysis Services, All Servers)               4/9/2014 12:00:01 AM EngineService Name=MSOLAP$POWERPIVOT  
Online Health Analysis Job (Hourly, SQL Server Analysis Services, All Servers)              4/9/2014 1:00:01 PM  EngineService Name=MSOLAP$POWERPIVOT  
Online Health Analysis Job (Weekly, SQL Server Analysis Services, All Servers)              4/6/2014 12:00:10 AM EngineService Name=MSOLAP$POWERPIVOT  
Online PowerPivot Management Dashboard Processing Timer Job                                 4/8/2014 3:45:38 AM  MidTierService  
Online PowerPivot Health Statistics Collector Timer Job                                     4/9/2014 1:00:12 PM  MidTierService  
Online PowerPivot Data Refresh Timer Job                                                    4/9/2014 1:09:36 PM  MidTierService  
Online Health Analysis Job (Daily, SQL Server PowerPivot Service Application, All Servers)  4/9/2014 12:00:00 AM MidTierService  
Online Health Analysis Job (Daily, SQL Server PowerPivot Service Application, Any Server)   4/9/2014 12:00:00 AM MidTierService  
Online Health Analysis Job (Weekly, SQL Server PowerPivot Service Application, All Servers) 4/6/2014 12:00:03 AM MidTierService  
Online Health Analysis Job (Weekly, SQL Server PowerPivot Service Application, Any Server)  4/6/2014 12:00:03 AM MidTierService  
Online PowerPivot Setup Extension Timer Job                                                 4/1/2014 1:40:31 AM  MidTierService  
```  
  
##  <a name="bkmk_health_rules"></a>Reglas de estado  
 Hay menos reglas en una implementación de SharePoint 2013. Para obtener una lista completa de reglas para cada entorno de SharePoint y una explicación de cómo usar las reglas, consulte [reglas de estado de PowerPivot-configurar](../../power-pivot-sharepoint/configure-power-pivot-health-rules.md).  
  
```powershell
Get-SPHealthAnalysisRule | Select name, enabled, summary | Where {$_.summary -Like "*power*"}  | Format-Table -Property * -AutoSize | Out-Default  
```
  
```Output
Name                          Enabled Summary  
----                          ------- -------           
SecondaryLogonHealthRule         True PowerPivot:  Secondary Logon service (seclogon) is disabled  
DataRefreshTimerJobHealthRule    True PowerPivot: The PowerPivot Data Refresh timer job is disabled.  
ASUsageLoadHealthRule            True PowerPivot: The ratio of load events to connections is too high.  
ASMiniDumpHealthRule             True PowerPivot: One or more minidump files were found in the Logs directory, indicating a program crash  
ASUsageCubeRule                  True PowerPivot: Usage data is not getting updated at the expected frequency.  
ASADOMDNETHealthRule             True PowerPivot: ADOMD.NET is not installed on a standalone WFE that is configured for central admin  
MidTierAcctReadPermissionRule    True PowerPivot: MidTier process account should have 'Full Read' permission on all associated SPWebApplications.  
```  
  
##  <a name="bkmk_logs"></a>Registros de Windows y ULS  
 **Registro de eventos de Windows**  
  
 El comando siguiente buscará en el registro de eventos de Windows los eventos relacionados con la instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] en modo de SharePoint. Para obtener información sobre cómo deshabilitar eventos o cambiar el nivel de evento, vea [configurar y ver archivos de registro de SharePoint y el registro de diagnósticos &#40;PowerPivot para SharePoint&#41;](../../power-pivot-sharepoint/configure-and-view-sharepoint-and-diagnostic-logging.md).  
  
 **Nombre del servicio:** MSOLAP $ POWERPIVOT  
  
 **Nombre para mostrar en servicios de Windows:** SQL Server Analysis Services (POWERPIVOT)  
  
```powershell
Get-EventLog "application" | Where-Object {$_.source -Like "msolap`$powerpivot*"}  | Select timegenerated, entrytype , source, message | Format-Table -property * -AutoSize | Out-Default  
```
  
```Output
TimeGenerated           EntryType Source            Message  
-------------           --------- ------            -------  
4/16/2014 1:45:19 PM  Information MSOLAP$POWERPIVOT Software usage metrics are disabled.  
4/16/2014 1:45:19 PM  Information MSOLAP$POWERPIVOT Service started. Microsoft SQL Server Analysis Services 64 Bit Evaluation (x64) RTM 12.0.1997.5.  
4/16/2014 1:45:18 PM  Information MSOLAP$POWERPIVOT The flight recorder was started.  
4/14/2014 6:45:37 PM  Information MSOLAP$POWERPIVOT Software usage metrics are disabled.  
```  
  
 **Registro de ULS de SharePoint, últimas 48 horas**  
  
 El comando siguiente devolverá mensajes de [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] del registro de ULS creados en las últimas 48 horas. Ajuste el parámetro addhours según sea necesario.  
  
```powershell
Get-SPLogEvent -StartTime(Get-Date).AddHours(-48) | Where-Object {$_.Area -eq "powerpivot service" -and $_.level -eq "high"} | Select timestamp, area, category, eventid,level, message | Format-Table -Property * -AutoSize | Out-Default  
```  
  
 La variación siguiente del comando solo devuelve eventos del registro para la categoría de **actualización de datos** .  
  
```powershell
Get-SPLogEvent -starttime(Get-Date).addhours(-48) | Where-Object {$_.category -eq "data refresh" -and $_.level -eq "high"} | Select timestamp, area, category, eventid, level, correlation, message  
```
  
```Output
Timestamp   : 4/14/2014 7:15:01 PM  
Area        : PowerPivot Service  
Category    : Data Refresh  
EventID     : 43  
Level       : High  
Correlation : 5755879c-7cab-e097-8f80-f27895d44a77  
Message     : The following error occurred when working with the service application, Default PowerPivot Service Application. Skipping the service application..  
  
Timestamp   : 4/14/2014 7:15:02 PM  
Area        : PowerPivot Service  
Category    : Data Refresh  
EventID     : 99  
Level       : High  
Correlation : 5755879c-7cab-e097-8f80-f27895d44a77  
Message     : EXCEPTION: System.TimeoutException: The request channel timed out while waiting for a reply after 00:00:47.0625313. Increase the timeout value passed to   
              the call to Request or increase the SendTimeout value on the Binding. The time allotted to this operation may have been a portion of a longer timeout.   
              ---> System.TimeoutException: The HTTP request to 'http://localhost:32843/SecurityTokenServiceApplication/securitytoken.svc/actas' has exceeded the   
              allotted timeout of 00:00:54.5930000. The time allotted to this operation may have been a portion of a longer timeout. ---> System.Net.WebException: The   
              operation has timed out     at System.Net.HttpWebRequest.GetResponse()     at   
              System.ServiceModel.Channels.HttpChannelFactory`1.HttpRequestChannel.HttpChannelRequest.WaitForReply(TimeSpan timeout...  
```  
  
##  <a name="bkmk_msolap"></a>Proveedor MSOLAP  
 Compruebe el proveedor MSOLAP. [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]y [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)] [!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)] requieren msolap. 5.  
  
```powershell
$excelApp = Get-SPExcelServiceApplication  
Get-SPExcelDataProvider -ExcelServiceApplication $excelApp | Select providerid, providertype, description | Where {$_.providerid -like "msolap*" } | Format-Table -Property * -AutoSize | Out-Default  
```
  
```Output
ProviderId ProviderType Description  
---------- ------------ -----------  
MSOLAP     Oledb        Microsoft OLE DB Provider for OLAP Services       
MSOLAP.3   Oledb        Microsoft OLE DB Provider for OLAP Services 9.0   
MSOLAP.4   Oledb        Microsoft OLE DB Provider for OLAP Services 10.0  
MSOLAP.5   Oledb        Microsoft OLE DB Provider for OLAP Services 11.0  
```  
  
 Para más información, consulte [Instalar el proveedor OLE DB de Analysis Services en servidores de SharePoint](../../../sql-server/install/install-the-analysis-services-ole-db-provider-on-sharepoint-servers.md) y [Agregar MSOLAP.5 como proveedor de datos de confianza en Excel Services](https://technet.microsoft.com/library/hh758436.aspx).  
  
##  <a name="bkmk_adomd"></a>Biblioteca de cliente de ADOMD.Net  
  
```powershell
Get-WMIObject -Class win32_product | Where-Object {$_.name -Like "*ado*"} | Select name, version, vendor | Format-Table -Property * -AutoSize | out-default  
```
  
```Output
name                                                  version      vendor  
----                                                  -------      ------  
Microsoft SQL Server 2008 Analysis Services ADOMD.NET 10.1.2531.0  Microsoft Corporation  
Microsoft SQL Server 2005 Analysis Services ADOMD.NET 9.00.1399.06 Microsoft Corporation  
```  
  
 Para obtener más información, vea [Instalar ADOMD.NET en servidores front-end web ejecutando Administración central](../../../sql-server/install/install-adomd-net-on-web-front-end-servers-running-central-administration.md).  
  
##  <a name="bkmk_health_collection"></a>Reglas de recopilación de datos de mantenimiento  
 Compruebe que el **Estado** está en línea y que **Habilitado** es True.  
  
```powershell
Get-SPUsageDefinition | Select name, status, enabled, tablename, DaysToKeepDetailedData | Where {$_.name -Like "powerpivot*"} | Format-Table -Property * -AutoSize | Out-Default  
```
  
```Output
Name                         Status Enabled TableName                   DaysToKeepDetailedData  
----                         ------ ------- ---------                   ----------------------  
PowerPivot Connections       OnlineTrue AnalysisServicesConnections  14  
PowerPivot Load Data Usage   Online    True AnalysisServicesLoads                           14  
PowerPivot Query Usage       Online    True AnalysisServicesRequests                        14  
PowerPivot Unload Data Usage Online    True AnalysisServicesUnloads                         14  
```  
  
 Para obtener más información, consulte [PowerPivot Usage Data Collection](../../power-pivot-sharepoint/power-pivot-usage-data-collection.md).  
  
##  <a name="bkmk_solutions"></a>Solución  
 Si los demás componentes están en línea, puede omitir la comprobación de las soluciones. Sin embargo, si faltan reglas de mantenimiento, compruebe que las dos soluciones existen y mostraban Compruebe que las dos soluciones de PowerPivot están **En línea** e **Implementada**.  
  
```powershell
Get-SPSolution | Select name, status, deployed, DeploymentState, DeployedServers | Where {$_.Name -Like "*powerpivot*"} | Format-Table -Property * -AutoSize | Out-Default  
```  
  
SharePoint 2013:
  
```Output
Name                                 Status Deployed        DeploymentState DeployedServers  
----                                 ------ --------        --------------- ---------------  
powerpivotfarm14solution.wsp         Online     True         GlobalDeployed {UETESTA00}  
powerpivotfarmsolution.wsp           Online     True         GlobalDeployed {UETESTA00}  
powerpivotwebapplicationsolution.wsp Online     True WebApplicationDeployed {UETESTA00}  
```  
  
SharePoint 2010:
  
```Output
Name                 Status Deployed        DeploymentState DeployedServers   
----                 ------ --------        --------------- ---------------   
powerpivotfarm.wsp   Online     True         GlobalDeployed {uesql11spoint2}  
powerpivotwebapp.wsp Online     True WebApplicationDeployed {uesql11spoint2}  
```  
  
 Para obtener más información sobre cómo implementar soluciones de SharePoint, vea [Implementación de paquetes de solución (SharePoint Server 2010)](https://technet.microsoft.com/library/cc262995\(v=office.14\).aspx).  
  
##  <a name="bkmk_manual"></a>Pasos de comprobación manual  
 En esta sección se describen los pasos de comprobación que no se pueden completar mediante cmdlets de PowerShell.  
  
 **Actualización de datos programada:** Configure la actualización programar un libro para que **también se actualice lo antes posible**.  Para obtener más información, vea la sección "comprobar la actualización de datos" de [programación de actualización de datos y orígenes de datos que no admiten la autenticación de Windows &#40;PowerPivot para SharePoint&#41;](../../power-pivot-sharepoint/schedule-data-refresh-and-data-sources-no-windows-authentication.md).  
  
##  <a name="bkmk_more_resources"></a>Más recursos  
 [Cmdlets de administración de servidor Web (IIS) en Windows PowerShell](https://technet.microsoft.com/library/ee790599.aspx).  
  
 [PowerShell para comprobar los servicios, los sitios IIS y el estado del grupo de aplicaciones en SharePoint](https://gallery.technet.microsoft.com/office/PowerShell-to-check-a6ed72a0).  
  
 [Referencia de Windows PowerShell para SharePoint 2013](https://technet.microsoft.com/library/ee890108\(v=office.15\).aspx)  
  
 [Referencia de Windows PowerShell para SharePoint Foundation 2010](https://technet.microsoft.com/library/ee890105\(v=office.14\).aspx)  
  
 [Administración de servicios de Excel con Windows PowerShell (SharePoint Server 2010)](https://technet.microsoft.com/library/ff191201\(v=office.14\).aspx)  
  
 [Ver y leer los archivos de registro de instalación de SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
 [Usar el cmdlet Get-EventLog](https://technet.microsoft.com/library/ee176846.aspx)  
  
##  <a name="bkmk_full_script"></a>Script completo de PowerShell  
 El siguiente script contiene todos los comandos de las secciones anteriores. El script ejecuta los comandos en el mismo orden en que se presentan en este tema. El script contiene alguna variaciones opcionales de los comandos indicadas en este tema por si necesita algún filtrado adicional. Las variaciones se deshabilitan con un carácter de comentario (#). El script también incluye algunas instrucciones para comprobar el modo de SharePoint de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] . Las instrucciones de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] se deshabilitan con un carácter de comentario (#).  
  
```powershell
# This script audits services related to PowerPivot for SharePoint  
$starttime = Get-Date  
write-host -foregroundcolor DarkGray StartTime $starttime
  
Write-Host  "Import the SharePoint PowerShell snappin"  
Add-PSSnapin Microsoft.Sharepoint.Powershell -EA 0  
  
Write-Host -ForegroundColor Green "Analysis Services Windows Service"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-Service | Select name, displayname, status | Where {$_.Name -eq "msolap`$powerpivot"} | Format-Table -Property * -AutoSize | Out-Default  
  
Write-Host -ForegroundColor Green "PowerPivotEngineService and PowerPivotSystemService"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
  
Get-PowerPivotSystemService | Select typename, status, applications, farm | Format-Table -property * -AutoSize | Out-Default  
# If needed, you can run the following to compare job definitions specific to the service against the results of the timer job definition section  
#Get-PowerPivotSystemService | select -ExpandProperty jobdefinitions | select displayname, schedule, service | format-table -property * -autosize | out-default  
  
Get-PowerPivotEngineService | Select typename, status, name, instances, farm | Format-Table -property * -AutoSize | Out-Default  
# If needed, you can run the following to compare job definitions specific to the service against the results of the timer job definition section  
#Get-PowerPivotEngineService | select -ExpandProperty jobdefinitions | select displayname, schedule, service | format-table -property * -autosize | out-default  

#Write-Host -ForegroundColor Green "Service Instances - optional if you want to associate services with the server"  
#Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
#Get-SPServiceInstance | select typename, status, server, service, instance | where {$_.TypeName -like "*powerpivot*" -or $_.TypeName -like "*excel*" -or $_.TypeName -like "*Analysis Services*"} | format-table -property * -autosize | out-default  
#Get-PowerPivotEngineServiceInstance  | select typename, ASServername, status, server, service, instance  
#Get-PowerPivotSystemServiceInstance  | select typename, ASSServerName, status, server, service, instance  

Write-Host -ForegroundColor Green "PowerPivot And Excel Service Applications"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-PowerPivotServiceApplication | Select typename,name, status, unattendedaccount, applicationpool, farm, database
Get-SPExcelServiceApplication | Select typename,  DisplayName, status
  
#Write-Host ""  
Write-Host -ForegroundColor Green "PowerPivot Service Application pool"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
# the following assumes there is only 1 PowerPivot Service Application, and returns that application's pool name.  if you have more than one, use the 2nd version  
$poolname = [string](Get-PowerPivotServiceApplication | Select -Property applicationpool)  
$position = $poolname.lastindexof("=")  
$poolname = $poolname.substring($position+1)  
$poolname = $poolname.substring(0,$poolname.length-1)  
Get-SPServiceApplicationPool | Select name, status, processaccountname, id | Where {$_.Name -eq $poolname} | Format-Table -Property * -AutoSize | Out-Default  
  
#Write-Host ""  
Write-Host -ForegroundColor Green "PowerPivot and Excel Service Application Proxy"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-SPServiceApplicationProxy |  Select typename, status, unattendedaccount, displayname | Where {$_.TypeName -like "*powerpivot*" -or $_.TypeName -like "*excel services*"} | Format-Table -Property * -AutoSize | Out-Default  
#Get-SPServiceApplicationProxy |  select typename, status, unattendedaccount, displayname | where {$_.TypeName -like "*powerpivot*" -or $_.TypeName -like "*Reporting Services*" -or $_.TypeName -like "*excel services*"} | format-table -property * -autosize | out-default  

Write-Host -ForegroundColor Green "DATABASES"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-SPDatabase | Select name, status, server, typename | Where {$_.TypeName -eq "content database" -or $_.TypeName -like "*Gemini*"} | Format-Table -Property * -AutoSize | Out-Default  
#Get-SPDatabase | select name, status, server, typename | where {$_.TypeName -eq "content database" -or $_.TypeName -like "*Gemini*" -or $_.TypeName -like "*ReportingServices*"}

Write-Host -ForegroundColor Green "features"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-SPFeature | Select displayname, status, scope, farm | Where {$_.displayName -like "*powerpivot*"} | Format-Table -Property * -AutoSize | Out-Default  
#Get-SPFeature | select displayname, status, scope, farm | where {$_.displayName -like "*powerpivot*" -or $_.displayName -like "*ReportServer*"}  | format-table -property * -autosize | out-default  

Write-Host -ForegroundColor Green "Timer Jobs (Job Definitions) -- list is the same as seen in the 'Review timer job definitions' section of the management dashboard"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-SPTimerJob | Where {$_.service -like "*power*" -or $_.service -like "*mid*"} | Select status, displayname, LastRunTime, service | Format-Table -Property * -AutoSize | Out-Default  

Write-Host -ForegroundColor Green "health rules"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-SPHealthAnalysisRule | Select name, enabled, summary | Where {$_.summary -Like "*power*"}  | Format-Table -Property * -AutoSize | Out-Default  
  
$time = Get-Date  
Write-Host -ForegroundColor DarkGray StartTime $starttime
Write-Host -ForegroundColor DarkGray EndTime $time  

Write-Host -ForegroundColor Green "Windows Event Log data MSSQL$POWERPIVOT and "  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-EventLog "application" | Where-Object {$_.source -like "msolap`$powerpivot*"}  | Select timegenerated, entrytype , source, message | Format-Table -Property * -autosize | Out-Default  
#The following is the same command but with the Inforamtion events filtered out.  
#Get-EventLog "application" | Where-Object {$_.source -like "msolap`$powerpivot*" -and ($_.entrytype -match "error" -or $_.entrytype -match "critical" -or $_.entrytype -match "warning")}  |select timegenerated, entrytype , source, message | format-table -property * -autosize | out-default  
  
#Write-Host ""  
Write-Host -ForegroundColor Green "ULS Log data"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-SPLogEvent -StartTime(Get-Date).AddHours(-48) | Where-Object {$_.Area -eq "powerpivot service" -and $_.level -eq "high"} | Select timestamp, area, category, eventid, level, correlation, message | Format-Table -Property * -AutoSize | Out-Default  
#the following example filters for the category 'data refresh'  
#Get-SPLogEvent -starttime(get-date).addhours(-48) | Where-Object {$_.category -eq "data refresh" -and $_.level -eq "high"} | select timestamp, area, category, eventid, level, correlation, message  
  
$time = Get-Date  
Write-Host -ForegroundColor DarkGray StartTime $starttime
Write-Host -ForegroundColor DarkGray EndTime $time  

Write-Host -ForegroundColor Green "MSOLAP data provider for Excel Servivces, service application"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
$excelApp = Get-SPExcelServiceApplication  
Get-SPExcelDataProvider -ExcelServiceApplication $excelApp | Select providerid, providertype, description | Where {$_.providerid -like "msolap*" } | Format-Table -Property * -AutoSize | Out-Default  
  
Write-Host -ForegroundColor Green "ADOMD.net client library"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-WMIObject -Class win32_product | Where-Object {$_.name -like "*ado*"} | Select name, version, vendor | Format-Table -Property * -AutoSize | Out-Default  
  
Write-Host -ForegroundColor Green "Usage Data Rules"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-SPUsageDefinition | Select name, status, enabled, tablename, DaysToKeepDetailedData | Where {$_.name -like "powerpivot*"} | Format-Table -Property * -AutoSize | Out-Default  
  
Write-Host -ForegroundColor Green "Solutions"  
Write-Host -ForegroundColor Green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"  
Get-SPSolution | Select name, status, deployed, DeploymentState, DeployedServers | Where {$_.Name -like "*powerpivot*"} | Format-Table -Property * -AutoSize | Out-Default  
  
$time = Get-Date  
Write-Host -ForegroundColor DarkGray StartTime $starttime
Write-Host -ForegroundColor DarkGray EndTime $time
