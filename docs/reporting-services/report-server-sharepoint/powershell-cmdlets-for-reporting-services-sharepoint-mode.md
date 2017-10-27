---
title: Cmdlets de PowerShell para el modo de SharePoint de Reporting Services | Documentos de Microsoft
ms.custom: 
ms.date: 09/25/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: ea362cd05de5d1ba17ca717d94354d5786119bab
ms.openlocfilehash: 5ab2078266bb130e80b0919c2a4f19e8cf45a671
ms.contentlocale: es-es
ms.lasthandoff: 10/06/2017

---
# <a name="powershell-cmdlets-for-reporting-services-sharepoint-mode"></a>Cmdlets de PowerShell para el modo de SharePoint de Reporting Services

[!INCLUDE[ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

Al instalar el modo de SharePoint de SQL Server 2016 Reporting Services, los cmdlets de PowerShell se instalan para admitir servidores de informes en modo de SharePoint. Los cmdlets abarcan tres categorías de funcionalidad.  
  
-   Proxy y el servicio compartido de instalación de Reporting Services SharePoint.  
  
-   Aprovisionamiento y administración de Reporting Services de servicio de aplicaciones y servidores proxy asociados.  
  
-   Administración de características de Reporting Services, para las claves de cifrado y las extensiones de ejemplo.  

> [!NOTE]
> Integración de Reporting Services con SharePoint ya no está disponible después de SQL Server 2016.

## <a name="cmdlet-summary"></a>Resumen de los cmdlets

 Para ejecutar los cmdlets es necesario abrir el Shell de administración de SharePoint. También puede usar el editor de la interfaz gráfica de usuario incluido en Microsoft Windows, **Entorno de scripting integrado (ISE) de Windows PowerShell**. Para más información, vea [Starting Windows PowerShell on Windows Server](http://technet.microsoft.com/library/hh847814.aspx). En los resúmenes siguientes de cmdlet, las referencias a 'bases de datos', se aplican a todas las bases de datos creadas y usadas por una aplicación de servicio de Reporting Services. Esto incluye la configuración, la creación de alertas y las bases de datos temporales.  
  
 Si ve un mensaje de error similar al siguiente al escribir los ejemplos de PowerShell:  
  
-   Install-SPRSService : El término 'Install-SPRSService' no se reconoce como  
    nombre de un cmdlet, función, archivo de script o programa ejecutable. Compruebe la ortografía del nombre o si una ruta de acceso se incluyó, compruebe que la ruta de acceso es correcta e inténtelo de nuevo.  
  
 Se está produciendo uno de los problemas siguientes:  
  
-   SharePoint de Reporting Services no está instalado y, por tanto, no se instalan los cmdlets de Reporting Services.  
  
-   Ejecutó el comando de PowerShell en Windows Powershell o Windows PowerShell ISE en lugar del Shell de administración de SharePoint. Use el Shell de administración de SharePoint o agregue el Complemento de SharePoint a la ventana de Windows PowerShell con el comando siguiente:  
  
    ```  
    Add-PSSnapin Microsoft.SharePoint.PowerShell  
    ```  
  
 Para más información, vea [Usar Windows PowerShell para administrar SharePoint 2013](http://technet.microsoft.com/library/ee806878.aspx).  
  
### <a name="open-the-sharepoint-management-shell-and-run-cmdlets"></a>Abra el Shell de administración de SharePoint y ejecutar los cmdlets
  
1.  Haga clic en el botón **Inicio** .  
  
2.  Haga clic en el grupo **Productos de Microsoft SharePoint** .  
  
3.  Haga clic en **Shell de administración de SharePoint**.  
  
 Para ver la ayuda de la línea de comandos para un cmdlet, utilice el comando ‘Get-Help’ de PowerShell en el símbolo del sistema de PowerShell. Por ejemplo:  
  
 `Get-Help Get-SPRSServiceApplicationServers`  
  
##  <a name="shared-service-and-proxy-cmdlets"></a>Cmdlets de proxy y el servicio compartido

 En la tabla siguiente contiene los cmdlets de PowerShell para el servicio de Reporting Services compartidas de SharePoint.  
  
|Cmdlet|Description|  
|------------|-----------------|  
|Install-SPRSService|Instala y registra o desinstala, el servicio compartido de Reporting Services. Esto puede hacerse únicamente en el equipo que tiene una instalación de SQL Server Reporting Services en modo de SharePoint. Para la instalación, se producen dos operaciones:<br /><br /> -El servicio de Reporting Services está instalado en la granja de servidores.<br /><br /> -La instancia de servicio de Reporting Services está instalada en el equipo actual.<br /><br /> Para la desinstalación, se producen dos operaciones:<br /><br /> -El servicio de Reporting Services se desinstala de la máquina actual.<br /><br /> -El servicio de Reporting Services se desinstala de la granja de servidores.<br /><br /> <br /><br /> Si hay otros equipos en la granja de servidores que tienen instalado el servicio de Reporting Services, o si todavía hay aplicaciones de servicio de Reporting Services ejecutándose en la granja, se muestra un mensaje de advertencia.|  
|Install-SPRSServiceProxy|Instala y registra, o desinstala, el proxy de servicio de Reporting Services en la granja de SharePoint.|  
|Get-SPRSProxyUrl|Obtiene las direcciones URL para obtener acceso al servicio de Reporting Services.|  
|Get-SPRSServiceApplicationServers|Obtiene todos los servidores de la granja de SharePoint que contienen una instalación del servicio compartido de Reporting Services. Este cmdlet es útil para las actualizaciones de Reporting Services, para determinar qué servidores ejecutan el servicio compartido y, por tanto, hay que actualizar.|  
  
## <a name="service-application-and-proxy-cmdlets"></a>Cmdlets de proxy y la aplicación de servicio

 En la tabla siguiente contiene los cmdlets de PowerShell para las aplicaciones de servicio de Reporting Services y sus servidores proxy asociados.  
  
|cmdlet|Description|  
|------------|-----------------|  
|Get-SPRSServiceApplication|Obtiene uno o varios objetos de aplicación de servicio de Reporting Services.|  
|New-SPRSServiceApplication|Crea una nueva aplicación de servicio de Reporting Services y las bases de datos asociadas.<br /><br /> Parámetro LogonType: especifica si el servidor de informes utiliza la cuenta del grupo de aplicaciones SSRS o un inicio de sesión de SQL Server para tener acceso a la base de datos del servidor de informes. Los valores válidos son:<br /><br /> 0 Autenticación de Windows<br /><br /> 1 SQL Server<br /><br /> 2 Cuenta del grupo de aplicaciones (valor predeterminado)|  
|Remove-SPRSServiceApplication|Quita la aplicación de servicio de Reporting Services especificada. También se quitarán las bases de datos asociadas.|  
|Set-SPRSServiceApplication|Edita las propiedades de una aplicación de servicio de Reporting Services existente.|  
|New-SPRSServiceApplicationProxy|Crea un nuevo proxy de aplicación de servicio de Reporting Services.|  
|Get-SPRSServiceApplicationProxy|Obtiene uno o más servidores proxy de aplicación de servicio de Reporting Services.|  
|Dismount-SPRSDatabase|Desmonta las bases de datos de aplicación de servicio para una aplicación de servicio de Reporting Services.|  
|Remove-SPRSDatabase|Quitar las bases de datos de aplicación de servicio para una aplicación de servicio de Reporting Services.|  
|Set-SPRSDatabase|Establece las propiedades de las bases de datos asociadas a una aplicación de servicio de Reporting Services.|  
|Mount-SPRSDatabase|Monta las bases de datos para una aplicación de servicio de Reporting Services.|  
|New-SPRSDatabase|Crear nuevas bases de datos de aplicación de servicio para la aplicación de servicio de Reporting Services especificada.|  
|Get-SPRSDatabaseCreationScript|Genera el script de creación de la base de datos en la pantalla para una aplicación de servicio de Reporting Services. Este script se puede ejecutar a continuación en SQL Server Management Studio.|  
|Get-SPRSDatabase|Obtiene una o más bases de datos de aplicación de servicio de Reporting Services. Use el comando para obtener el identificador de la base de datos de la aplicación del servicio de forma que pueda usar el cmdlet Set-SPRSDatabase para modificar las propiedades, por ejemplo `querytimeout`. Vea el ejemplo de este tema, [Obtener y establecer las propiedades de la base de datos de aplicación de Reporting Services](#bkmk_example_db_properties).|  
|Get-SPRSDatabaseRightsScript|Genera el script de permisos de base de datos en la pantalla para una aplicación de servicio de Reporting Services. Solicita el usuario y la base de datos, y luego devuelve Transact-SQL que se puede ejecutar para modificar los permisos. Este script se puede ejecutar a continuación en SQL Server Management Studio.|  
|Get-SPRSDatabaseUpgradeScript|Muestra el script de actualización de bases de datos en la pantalla. El script actualizará las bases de datos de aplicación de servicio de Reporting Services a la versión de base de datos de la instalación de Reporting Services actual.|  
  
## <a name="reporting-services-custom-runctionality-cmdlets"></a>Cmdlets de Reporting Services runctionality personalizado
  
|Cmdlet|Description|  
|------------|-----------------|  
|Update-SPRSEncryptionKey|Actualiza la clave de cifrado para la aplicación de servicio de Reporting Services especificada y cifra de nuevo sus datos.|  
|Restore-SPRSEncryptionKey|Restaura una clave de cifrado de la que se hizo copia de seguridad anteriormente para una aplicación de servicio de Reporting Services.|  
|Remove-SPRSEncryptedData|Elimina los datos cifrados para la aplicación de servicio de Reporting Services especificada.|  
|Backup-SPRSEncryptionKey|Realiza una copia de seguridad de la clave de cifrado para la aplicación de servicio de Reporting Services especificada.|  
|New-SPRSExtension|Registra una nueva extensión con una aplicación de servicio de Reporting Services.|  
|Set-SPRSExtension|Establece las propiedades de una extensión de Reporting Services existente.|  
|Remove-SPRSExtension|Quita una extensión de una aplicación de servicio de Reporting Services.|  
|Get-SPRSExtension|Obtiene una o más extensiones de Reporting Services para un aplicación de servicio de Reporting Services.<br /><br /> Los valores válidos son:<br /><br /> <br /><br /> Entrega<br /><br /> DeliveryUI<br /><br /> Render<br /><br /> Datos<br /><br /> Seguridad<br /><br /> Autenticación<br /><br /> EventProcessing<br /><br /> ReportItems<br /><br /> Diseñador<br /><br /> ReportItemDesigner<br /><br /> ReportItemConverter<br /><br /> ReportDefinitionCustomization|  
|Get-SPRSSite|Obtiene los sitios de SharePoint basándose en si está habilitada la característica "ReportingService". De forma predeterminada, se devuelven los sitios que habilitan la característica "ReportingService".|  
  
## <a name="basic-samples"></a>Ejemplos básicos

 Devolver una lista de cmdlets cuyo nombre contiene ‘SPRS’. Se trata de la lista completa de cmdlets de Reporting Services.  
  
```  
Get-command –noun *SPRS*  
```  
  
 O con un poco más detalle, enviar la salida a un archivo de texto denominado commandlist.txt  
  
```  
Get-command -noun *SPRS* | Select name, definition | Format-List | Out-File c:\commandlist.txt  
```  
  
 Instalar el servicio de SharePoint de Reporting Services y el proxy de servicio.  
  
```  
Install-SPRSService  
```  
  
```  
Install-SPRSServiceProxy  
```  
  
 Iniciar el servicio de Reporting Services  
  
```  
get-spserviceinstance -all |where {$_.TypeName -like "SQL Server Reporting*"} | Start-SPServiceInstance  
```  
  
 Escriba el siguiente comando desde el Shell de administración de SharePoint para devolver una lista filtrada de filas de un archivo de registro. El comando filtrará las líneas que contengan “ssrscustomactionerror”. En este ejemplo se examina el archivo de registro creado cuando se instaló rssharepoint.msi.  
  
```  
Get-content -path C:\Users\testuser\AppData\Local\Temp\rs_sp_0.log | select-string "ssrscustomactionerror"  
```  
  
## <a name="detailed-samples"></a>Ejemplos detallados

 Además de los ejemplos siguientes, vea la sección “Scripts de Windows PowerShell” en el tema [Windows PowerShell script for Steps 1–4](../../reporting-services/install-windows/install-the-first-report-server-in-sharepoint-mode.md#bkmk_full_script).  
  
### <a name="create-a-reporting-services-service-application-and-proxy"></a>Crear una aplicación de servicio de Reporting Services y un proxy

 Este script de ejemplo realiza las tareas siguientes:  
  
1.  Crea una aplicación de servicio de Reporting Services y un proxy. El script asume que el grupo de aplicaciones “My App Pool” ya existe.  
  
2.  Agrega el proxy al grupo de servidores proxy predeterminado.  
  
3.  Concede acceso a la aplicación de servicio al puerto 80 de la base de datos de contenido de la aplicación web. El script se da por supuesto sitio `http://sitename` ya existe.  
  
```  
# Create service application and service application proxy  
$appPool = Get-SPServiceApplicationPool “My App Pool”  
$serviceApp = New-SPRSServiceApplication “My RS Service App” –ApplicationPool $appPool  
$serviceAppProxy = New-SPRSServiceApplicationProxy –Name “My RS Service App Proxy” –ServiceApplication $serviceApp  
  
# Add service application proxy to default proxy group.  Any web application that uses the default proxy group will now be able to use this service application.  
Get-SPServiceApplicationProxyGroup –default | Add-SPServiceApplicationProxyGroupMember –Member $serviceAppProxy  
  
# Grant application pool account access to the port 80 web application’s content database.  
$webApp = Get-SPWebApplication “http://sitename”  
$appPoolAccountName = $appPool.ProcessAccount.LookupName()  
$webApp.GrantAccessToProcessIdentity($appPoolAccountName)  
  
```  
  
### <a name="review-and-update-a-reporting-services-delivery-extension"></a>Revisar y actualizar una extensión de entrega de Reporting Services

 El siguiente ejemplo de script de PowerShell actualiza la configuración de la extensión de entrega de correo electrónico del servidor de informes para la aplicación de servicio denominada `My RS Service App`. Actualice los valores para el servidor SMTP (`<email server name>`) y el alias de correo electrónico FROM (`<your FROM email address>`).  
  
```  
$app=get-sprsserviceapplication -Name "My RS Service App"  
$emailCfg = Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml   
$emailXml = [xml]$emailCfg   
$emailXml.SelectSingleNode("//SMTPServer").InnerText = “<email server name>”  
$emailXml.SelectSingleNode("//SendUsing").InnerText = "2"  
$emailXml.SelectSingleNode("//SMTPAuthenticate").InnerText = "2"  
$emailXml.SelectSingleNode("//From").InnerText = '<your FROM email address>'  
Set-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" -ExtensionConfiguration $emailXml.OuterXml  
```  
  
 En el ejemplo anterior, si no supiera el nombre exacto de la aplicación de servicio, podría reescribir la primera instrucción para obtener la aplicación de servicio a partir de una búsqueda del nombre parcial. Por ejemplo:  
  
```  
$app=get-sprsserviceapplication | where {$_.name -like " ssrs_testapp *"}  
```  
  
 El siguiente script devolverá los valores de la configuración actual de la extensión de entrega por correo electrónico del servidor de informes para la aplicación de servicio denominada “Reporting Services Application”. El primer paso establece el valor de la variable $app en el objeto de la aplicación de servicio denominada " My RS Service App "  
  
 La segunda instrucción obtendrá la extensión de entrega por correo electrónico del servidor de informes para el objeto de aplicación de servicio de la variable $app, y seleccionará el XML de configuración.  
  
```  
$app=get-sprsserviceapplication –Name "Reporting Services Application"  
Get-SPRSExtension -identity $app -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml  
```  
  
 Asimismo, puede reescribir las dos instrucciones anteriores como una sola:  
  
```  
get-sprsserviceapplication –Name "Reporting Services Application" | Get-SPRSExtension -ExtensionType "Delivery" -name "Report Server Email" | select -ExpandProperty ConfigurationXml  
```  
  
### <a name="get-and-set-properties-of-the-reporting-service-application-database"></a>Obtener y establecer las propiedades de la base de datos de aplicación de servicio de informes

 En el siguiente ejemplo, se obtiene, en primer lugar, una lista de las bases de datos y propiedades de forma que pueda determinar el GUID (identificador) de la base de datos que proporciona después al comando SET. Para obtener una lista completa de las propiedades, use `Get-SPRSDatabase | format-list`.  
  
```  
get-SPRSDatabase | select id, querytimeout,connectiontimeout, status, server, ServiceInstance   
```  
  
 A continuación se muestra un ejemplo del resultado. Determine el identificador para la base de datos que desee modificar y use el identificador en el cmdlet SET.  
  
-   `Id                : 56f8d1bc-cb04-44cf-bd41-a873643c5a14`  
  
     `QueryTimeout      : 120`  
  
     `ConnectionTimeout : 15`  
  
     `Status            : Online`  
  
     `Server            : SPServer Name=uetestb01`  
  
     `ServiceInstance   : SPDatabaseServiceInstance`  
  
```  
Set-SPRSDatabase –identity 56f8d1bc-cb04-44cf-bd41-a873643c5a14 -QueryTimeout 300  
```  
  
 Para comprobar que se ha establecido el valor, vuelva a ejecutar el cmdlet GET.  
  
```  
Get-SPRSDatabase –identity 56f8d1bc-cb04-44cf-bd41-a873643c5a14 | select id, querytimeout,connectiontimeout, status, server, ServiceInstance  
```  
  
### <a name="list-reporting-services-data-extensions"></a>Enumerar extensiones de datos de Reporting Services

 En el ejemplo siguiente se recorre en bucle cada aplicación de servicio de Reporting Services y enumera las extensiones de datos actual para cada uno.  
  
```  
$apps = Get-SPRSServiceApplication  
foreach ($app in $apps)   
{  
Write-host -ForegroundColor "yellow" Service App Name $app.Name  
Get-SPRSExtension -identity $app -ExtensionType “Data” | select name,extensiontype | Format-Table -AutoSize  
}  
```  
  
 **Salida de ejemplo:**  
  
-   `Name           ExtensionType`  
  
     `----           -------------`  
  
     `SQL                     Data`  
  
     `SQLAZURE                Data`  
  
     `SQLPDW                  Data`  
  
     `OLEDB                   Data`  
  
     `OLEDB-MD                Data`  
  
     `ORACLE                  Data`  
  
     `ODBC                    Data`  
  
     `XML                     Data`  
  
     `SHAREPOINTLIST          Data`  
  
### <a name="change-and-list-reporting-services-subscription-owners"></a>Cambiar y enumerar propietarios de suscripciones de Reporting Services

 Vea [usar PowerShell para cambiar y enumerar propietarios de suscripciones de Reporting Services y ejecutar una suscripción](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md).  
  
## <a name="next-steps"></a>Pasos siguientes

[Usar PowerShell para cambiar y enumerar propietarios de suscripciones de Reporting Services y ejecutar una suscripción](../../reporting-services/subscriptions/manage-subscription-owners-and-run-subscription-powershell.md)  
[Lista de comprobación: Usar PowerShell para comprobar PowerPivot para SharePoint](../../analysis-services/instances/install-windows/checklist-use-powershell-to-verify-power-pivot-for-sharepoint.md)   
[Get help SQL Server PowerShell](../../relational-databases/scripting/get-help-sql-server-powershell.md)   

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231).

