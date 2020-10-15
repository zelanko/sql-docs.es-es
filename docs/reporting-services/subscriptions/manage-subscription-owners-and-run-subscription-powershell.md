---
title: Administrar propietarios de suscripciones y ejecutar suscripciones (PowerShell) | Microsoft Docs
description: Aprenda a transferir mediante programación la propiedad de una suscripción a Reporting Services de un usuario a otro.
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: subscriptions
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.reviewer: ''
ms.custom: ''
ms.date: 01/16/2020
ms.openlocfilehash: b0174f0b7705c9a7c7c678782a4b17fb4a1a74af
ms.sourcegitcommit: a41e1f4199785a2b8019a419a1f3dcdc15571044
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2020
ms.locfileid: "91985921"
---
# <a name="manage-subscription-owners-and-run-subscription---powershell"></a>Administrar propietarios de suscripciones y ejecutar suscripciones (PowerShell)

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

A partir de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , se puede transferir mediante programación la propiedad de una suscripción a [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] de un usuario a otro. En este tema se proporcionan varios scripts de Windows PowerShell que puede utilizar para cambiar o simplemente presentar la propiedad de la suscripción. Cada ejemplo incluye sintaxis de ejemplo para el modo nativo y para el modo SharePoint. Después de cambiar el propietario de la suscripción, la suscripción se ejecutará en el contexto de seguridad del nuevo propietario, y el campo User!UserID del informe mostrará el valor del nuevo propietario. Para obtener más información sobre el modelo de objetos al que llaman los ejemplos de PowerShell, vea <xref:ReportService2010.ReportingService2010.ChangeSubscriptionOwner%2A>  

![Contenido relacionado con PowerShell](/analysis-services/analysis-services/instances/install-windows/media/rs-powershellicon.jpg "Contenido relacionado con PowerShell")

##  <a name="in-this-topic"></a><a name="bkmk_top"></a> En este tema:
  
- [Cómo usar los scripts](#bkmk_how_to)  
  
- [Script: Presenta la propiedad de todas las suscripciones](#bkmk_list_ownership_all)  
  
- [Script: Presenta todas las suscripciones poseídas por un usuario específico](#bkmk_list_all_one_user)  
  
- [Script: Cambia la propiedad de todas las suscripciones poseídas por un usuario específico](#bkmk_change_all)  
  
- [Script: Presenta todas las suscripciones asociadas a un informe específico](#bkmk_list_for_1_report)  
  
- [Script: Cambia la propiedad de una suscripción específica](#bkmk_change_all_1_subscription)  
  
- [Script: Ejecuta (desencadena) una suscripción única](#bkmk_run_1_subscription)  
  
## <a name="how-to-use-the-scripts"></a><a name="bkmk_how_to"></a> Cómo usar los scripts
  
### <a name="permissions"></a>Permisos

Esta sección resume los niveles de permiso requeridos para utilizar los métodos para el modo nativo y para el modo SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Los scripts de este tema usan los siguientes métodos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :  
  
- [Método ReportingService2010.ListSubscriptions](/dotnet/api/reportservice2010.reportingservice2010.listsubscriptions)  
  
- [Método ReportingService2010.ChangeSubscriptionOwner](/dotnet/api/reportservice2010.reportingservice2010.changesubscriptionowner)  
  
- [ReportingService2010.ListChildren](/dotnet/api/reportservice2010.reportingservice2010.listchildren)  
  
- El método [ReportingService2010.FireEvent](/dotnet/api/reportservice2010.reportingservice2010.fireevent) solo se usa en el último script para activar la suscripción específica que se ejecutará. Si no tiene previsto usar este script, puede omitir los requisitos de permisos para el método FireEvent.  
  
**Modo nativo:**
  
- Presentar suscripciones: [enumeración ReportOperation](/dotnet/api/microsoft.reportingservices.interfaces.reportoperation) en el informe Y el usuario es el propietario de la suscripción) O ReadAnySubscription.  
  
- Cambiar suscripciones: El usuario debe ser miembro del grupo BUILTIN\Administrators  
  
- Presentar elementos secundarios: ReadProperties en el elemento  
  
- Desencadenar evento: GenerateEvents (sistema)  
  
 **Modo SharePoint:**
  
- Presentar suscripciones: ManageAlerts O [CreateAlerts](/previous-versions/office/sharepoint-server/ms412690(v=office.15)) en el informe Y el usuario es el propietario de la suscripción y la suscripción es una suscripción programada).  
  
- Cambiar suscripciones: ManageWeb  
  
- Presentar elementos secundarios: ViewListItems  
  
- Desencadenar evento: ManageWeb  
  
 Para obtener más información, vea [Comparación de roles y tareas en Reporting Services con grupos y permisos de SharePoint](../../reporting-services/security/reporting-services-roles-tasks-vs-sharepoint-groups-permissions.md).  
  
### <a name="script-usage"></a>Uso de scripts

**Crear archivos de script (.ps1)**
  
1. Crear una carpeta con el nombre **c:\scripts**. Si elige una carpeta diferente, modifique el nombre de la carpeta usada en las instrucciones de sintaxis de línea de comandos del ejemplo.  
  
2. Cree un archivo de texto para cada script y guarde los archivos en la carpeta c:\scripts. Cuando cree los archivos .ps1, use el nombre de la sintaxis de línea de comandos de cada ejemplo.  
  
3. Abra un símbolo del sistema con privilegio de administración.  
  
4. Ejecute cada archivo de script utilizando la sintaxis de línea de comando proporcionada con cada ejemplo.  
  
**Entornos probados**
  
 Los scripts de este tema se probaron en PowerShell versión 3 y con las siguientes versiones de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]:  
  
- [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
- [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
- [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
## <a name="script-list-the-ownership-of-all-subscriptions"></a><a name="bkmk_list_ownership_all"></a> Script: Presenta la propiedad de todas las suscripciones

Este script presenta todas las suscripciones de un sitio. Puede usarlo para probar su conexión o para comprobar la ruta de acceso del informe y el identificador de la suscripción para su uso en los demás scripts. Además, es un script útil para verificar qué suscripciones existen y quién las posee.  
  
 **Sintaxis de modo nativo:**
  
```powershell
powershell c:\scripts\ListAll_SSRS_Subscriptions.ps1 "[server]/reportserver" "/"  
```  
  
 **Sintaxis de modo SharePoint:**
  
```powershell
powershell c:\scripts\ListAll_SSRS_Subscriptions.ps1 "[server]/_vti_bin/reportserver" "https://[server]"  
```  
  
 **Script:**
  
```
# Parameters  
#    server   - server and instance name (e.g. myserver/reportserver or myserver/reportserver_db2)  
  
Param(  
    [string]$server,  
    [string]$site  
   )  
  
$rs2010 += New-WebServiceProxy -Uri "https://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;  
$subscriptions += $rs2010.ListSubscriptions($site); # use "/" for default native mode site  
  
Write-Host " "  
Write-Host "----- $server's Subscriptions: "  
$subscriptions | select Path, report, Description, Owner, SubscriptionID, lastexecuted, Status  
```  
  
> [!TIP]  
> Para comprobar las direcciones URL de los sitios en modo de SharePoint, use el cmdlet de SharePoint **Get-SPSite**. Para obtener más información, vea [Get-SPSite](https://msdn.microsoft.com/library/ff607950\(v=office.15\).aspx).  
  
##  <a name="script-list-all-subscriptions-owned-by-a-specific-user"></a><a name="bkmk_list_all_one_user"></a> Script: Presenta todas las suscripciones poseídas por un usuario específico

Este script presenta todas las suscripciones poseídas por un usuario específico. Puede usarlo para probar su conexión o para comprobar la ruta de acceso del informe y el identificador de la suscripción para su uso en los demás scripts. Este script es útil si desea comprobar qué suscripciones poseía una persona que abandona su organización, para cambiar el propietario o eliminar la suscripción.  
  
 **Sintaxis de modo nativo:**
  
```powershell
powershell c:\scripts\ListAll_SSRS_Subscriptions4User.ps1 "[Domain]\[user]" "[server]/reportserver" "/"  
```  
  
**Sintaxis de modo SharePoint:**
  
```powershell
powershell c:\scripts\ListAll_SSRS_Subscriptions4User.ps1 "[Domain]\[user]"  "[server]/_vti_bin/reportserver" "https://[server]"  
```  
  
**Script:**
  
```
# Parameters:  
#    currentOwner - DOMAIN\USER that owns the subscriptions you wish to change  
#    server        - server and instance name (e.g. myserver/reportserver or myserver/reportserver_db2)  
#    site        - use "/" for default native mode site  
Param(  
    [string]$currentOwner,  
    [string]$server,  
    [string]$site  
)  
  
$rs2010 = New-WebServiceProxy -Uri "https://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;  
$subscriptions += $rs2010.ListSubscriptions($site);  
  
Write-Host " "  
Write-Host " "  
Write-Host "----- $currentOwner's Subscriptions: "  
$subscriptions | select Path, report, Description, Owner, SubscriptionID, lastexecuted,Status | where {$_.owner -eq $currentOwner}  
```  
  
## <a name="script-change-ownership-for-all-subscriptions-owned-by-a-specific-user"></a><a name="bkmk_change_all"></a> Script: Cambia la propiedad de todas las suscripciones poseídas por un usuario específico

Este script cambia la propiedad de todas las suscripciones poseídas por un usuario específico al nuevo parámetro de propietario.  
  
**Sintaxis de modo nativo:**  
  
```powershell
powershell c:\scripts\ChangeALL_SSRS_SubscriptionOwner.ps1 "[Domain]\current owner]" "[Domain]\[new owner]" "[server]/reportserver"  
```  
  
**Sintaxis de modo SharePoint:**  
  
```powershell
powershell c:\scripts\ChangeALL_SSRS_SubscriptionOwner.ps1 "[Domain]\{current owner]" "[Domain]\[new owner]" "[server]/_vti_bin/reportserver"  
```  
  
**Script:**  
  
```
# Parameters:  
#    currentOwner - DOMAIN\USER that owns the subscriptions you wish to change  
#    newOwner      - DOMAIN\USER that will own the subscriptions you wish to change  
#    server        - server and instance name (e.g. myserver/reportserver, myserver/reportserver_db2, myserver/_vti_bin/reportserver)
  
Param(  
    [string]$currentOwner,  
    [string]$newOwner,  
    [string]$server  
)  
  
$rs2010 = New-WebServiceProxy -Uri "https://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;  
$items = $rs2010.ListChildren("/", $true);  
  
$subscriptions = @();  
  
ForEach ($item in $items)  
{  
    if ($item.TypeName -eq "Report")  
    {  
        $curRepSubs = $rs2010.ListSubscriptions($item.Path);  
        ForEach ($curRepSub in $curRepSubs)  
        {  
            if ($curRepSub.Owner -eq $currentOwner)  
            {  
                $subscriptions += $curRepSub;  
            }  
        }  
    }  
}  
  
Write-Host " "  
Write-Host " "  
Write-Host -foregroundcolor "green" "-----  $currentOwner's Subscriptions changing ownership to $newOwner : "  
$subscriptions | select SubscriptionID, Owner, Path, Description,  Status  | format-table -AutoSize  
  
ForEach ($sub in $subscriptions)  
{  
    $rs2010.ChangeSubscriptionOwner($sub.SubscriptionID, $newOwner);  
}  
  
$subs2 = @();  
  
ForEach ($item in $items)  
{  
    if ($item.TypeName -eq "Report")  
    {  
        $subs2 += $rs2010.ListSubscriptions($item.Path);  
    }  
}  
```  
  
## <a name="script-list-all-subscriptions-associated-with-a-specific-report"></a><a name="bkmk_list_for_1_report"></a> Script: Presenta todas las suscripciones asociadas a un informe específico  

Este script presenta todas las suscripciones asociadas a un informe específico. La sintaxis de la ruta de acceso del informe es un modo de SharePoint diferente que requiere una dirección URL completa. En los ejemplos de sintaxis, el nombre del informe es "title only", que contiene un espacio, lo que obliga a usar comillas en el nombre del informe.  
  
**Sintaxis de modo nativo:**  
  
```powershell
powershell c:\scripts\List_SSRS_One_Reports_Subscriptions.ps1 "[server]/reportserver" "'/reports/title only'" "/"  
```  
  
**Sintaxis de modo SharePoint:**  
  
```powershell
powershell c:\scripts\List_SSRS_One_Reports_Subscriptions.ps1 "[server]/_vti_bin/reportserver"  "'https://[server]/shared documents/title only.rdl'" "https://[server]"  
```  
  
**Script:**  
  
```
# Parameters:  
#    server      - server and instance name (e.g. myserver/reportserver or myserver/reportserver_db2)  
#    reportpath  - path to report in the report server, including report name e.g. /reports/test report >> pass in  "'/reports/title only'"  
#    site        - use "/" for default native mode site  
Param  
(  
      [string]$server,  
      [string]$reportpath,  
      [string]$site  
)  
  
$rs2010 = New-WebServiceProxy -Uri "https://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;  
$subscriptions += $rs2010.ListSubscriptions($site);  
  
Write-Host " "  
Write-Host " "  
Write-Host "----- $reportpath 's Subscriptions: "  
$subscriptions | select Path, report, Description, Owner, SubscriptionID, lastexecuted,Status | where {$_.path -eq $reportpath}  
```  
  
## <a name="script-change-ownership-of-a-specific-subscription"></a><a name="bkmk_change_all_1_subscription"></a> Script: Cambia la propiedad de una suscripción específica  
 Este script cambia la propiedad de una suscripción específica. La suscripción está identificada por el SubscriptionID que pasa al script. Puede utilizar uno de los scripts para presentar suscripciones para determinar el SubscriptionID correcto.  
  
 **Sintaxis de modo nativo:**  
  
```powershell
powershell c:\scripts\Change_SSRS_Owner_One_Subscription.ps1 "[Domain]\[new owner]" "[server]/reportserver" "/" "ac5637a1-9982-4d89-9d69-a72a9c3b3150"  
```  
  
 **Sintaxis de modo SharePoint:**  
  
```powershell
powershell c:\scripts\Change_SSRS_Owner_One_Subscription.ps1 "[Domain]\[new owner]" "[server]/_vti_bin/reportserver" "https://[server]" "9660674b-f020-453f-b1e3-d9ba37624519"  
```  
  
 **Script:**  
  
```
# Parameters:  
#    newOwner       - DOMAIN\USER that will own the subscriptions you wish to change  
#    server         - server and instance name (e.g. myserver/reportserver or myserver/reportserver_db2)  
#    site        - use "/" for default native mode site  
#    subscriptionID - guid for the single subscription to change  
  
Param(  
    [string]$newOwner,  
    [string]$server,  
    [string]$site,  
    [string]$subscriptionid  
   )  
$rs2010 = New-WebServiceProxy -Uri "https://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential;  
  
$subscription += $rs2010.ListSubscriptions($site) | where {$_.SubscriptionID -eq $subscriptionid};  
  
Write-Host " "  
Write-Host "----- $subscriptionid's Subscription properties: "  
$subscription | select Path, report, Description, SubscriptionID, Owner, Status  
  
$rs2010.ChangeSubscriptionOwner($subscription.SubscriptionID, $newOwner)  
  
#refresh the list  
$subscription = $rs2010.ListSubscriptions($site) | where {$_.SubscriptionID -eq $subscriptionid}; # use "/" for default native mode site  
Write-Host "----- $subscriptionid's Subscription properties: "  
$subscription | select Path, report, Description, SubscriptionID, Owner, Status  
```  
  
## <a name="script-run-fire-a-single-subscription"></a><a name="bkmk_run_1_subscription"></a> Script: Ejecuta (desencadena) una sola suscripción  

Este script ejecuta una suscripción específica mediante el método FireEvent. El script ejecuta inmediatamente la suscripción independientemente de la programación configurada para la suscripción. Se compara EventType con el conjunto de eventos conocido que se ha definido en el archivo de configurador del servidor de informes **rsreportserver.config** . El script utiliza el siguiente tipo de eventos para las suscripciones estándar:  
  
 `<Event>`  
  
 `<Type>TimedSubscription</Type>`  
  
 `</Event>`  
  
 Para obtener más información acerca del archivo de configuración, consulte [RsReportServer.config Configuration File](../../reporting-services/report-server/rsreportserver-config-configuration-file.md).  
  
 El script incluye la lógica de retraso "`Start-Sleep -s 6`" para que haya tiempo después de que se desencadene el evento, de modo que el estado actualizado esté disponible con el método ListSubscription.  
  
 **Sintaxis de modo nativo:**  
  
```powershell
powershell c:\scripts\FireSubscription.ps1 "[server]/reportserver" $null "70366e82-2d3c-4edd-a216-b97e51e26de9"  
```  
  
 **Sintaxis de modo SharePoint:**  
  
```powershell
powershell c:\scripts\FireSubscription.ps1 "[server]/_vti_bin/reportserver" "https://[server]" "c3425c72-580d-423e-805a-41cf9799fd25"  
```  
  
 **Script:**  
  
```
  
# Parameters  
#    server         - server and instance name (e.g. myserver/reportserver or myserver/reportserver_db2)  
#    site           - use $null for a native mode server  
#    subscriptionid - subscription guid  
  
Param(  
  [string]$server,  
  [string]$site,  
  [string]$subscriptionid  
  )  
  
$rs2010 = New-WebServiceProxy -Uri "https://$server/ReportService2010.asmx" -Namespace SSRS.ReportingService2010 -UseDefaultCredential ;  
#event type is case sensative to what is in the rsreportserver.config  
$rs2010.FireEvent("TimedSubscription",$subscriptionid,$site)  
  
Write-Host " "  
Write-Host "----- Subscription ($subscriptionid) status: "  
#get list of subscriptions and filter to the specific ID to see the Status and LastExecuted  
Start-Sleep -s 6 # slight delay in processing so ListSubscription returns the updated Status and LastExecuted  
$subscriptions = $rs2010.ListSubscriptions($site);   
$subscriptions | select Status, Path, report, Description, Owner, SubscriptionID, EventType, lastexecuted | where {$_.SubscriptionID -eq $subscriptionid}  
  
```  

## <a name="see-also"></a>Consulte también  

- [Método ReportingService2010.ListSubscriptions](/dotnet/api/reportservice2010.reportingservice2010.listsubscriptions)  

- [Método ReportingService2010.ChangeSubscriptionOwner](/dotnet/api/reportservice2010.reportingservice2010.changesubscriptionowner)   

- [ReportingService2010.ListChildren](/dotnet/api/reportservice2010.reportingservice2010.listchildren)  

- [ReportingService2010.FireEvent](/dotnet/api/reportservice2010.reportingservice2010.fireevent)