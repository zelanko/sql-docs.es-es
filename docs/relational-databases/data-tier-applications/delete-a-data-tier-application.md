---
title: "Eliminación de una aplicación de capa de datos | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-data-tier-apps
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.deletedacwizard.deletedac.f1
- sql13.swb.deletedacwizard.summary.f1
- sql13.swb.deletedacwizard.introduction.f1
- sql13.swb.deletedacwizard.choosemethod.f1
helpviewer_keywords:
- How to [DAC], delete
- data-tier application [SQL Server], delete
- wizard [DAC], delete
- delete DAC
ms.assetid: 16fe1c18-4486-424d-81d6-d276ed97482f
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a6c69a8bbd4fa63a427658ddc7b8fdbd79b0af3b
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="delete-a-data-tier-application"></a>Eliminar una aplicación de capa de datos
  Puede eliminar una aplicación de capa de datos mediante el Asistente para eliminar aplicación de capa de datos o un script de Windows PowerShell. Puede especificar si la base de datos asociada se conserva, se separa o se quita.  
  
-   **Before you begin:**  [Limitations and Restrictions](#LimitationsRestrictions), [Permissions](#Permissions)  
  
-   **To upgrade a DAC, using:**  [The Register Data-tier Application Wizard](#UsingDeleteDACWizard), [PowerShell](#DeleteDACPowerShell)  
  
## <a name="before-you-begin"></a>Antes de empezar  
 Cuando elimine una instancia de la aplicación de capa de datos (DAC), elija una de tres opciones que especifican lo que se va a hacer con la base de datos asociada a la aplicación de capa de datos. Las tres opciones eliminan los metadatos de la definición de DAC. Las opciones difieren en lo que hacen con la base de datos asociada a la aplicación de capa de datos. El asistente no elimina ninguno de los objetos del nivel de instancia asociado a la DAC o la base de datos, como los inicios de sesión.  
  
|Opción|Acciones de base de datos|  
|------------|----------------------|  
|Eliminar registro|La base de datos asociada permanece intacta.|  
|Separar base de datos|La base de datos asociada se separa. La instancia del motor de base de datos no puede hacer referencia a la base de datos, pero los archivos de registro y de datos están intactos.|  
|Eliminar base de datos|Se quita la base de datos asociada. Se eliminan los archivos de registro y datos.|  
  
###  <a name="LimitationsRestrictions"></a> Limitaciones y restricciones  
 No hay ningún mecanismo automático para restaurar los metadatos o la base de datos de una DAC si esta se elimina. La forma de volver a generar manualmente la instancia de la DAC depende de la opción de eliminación.  
  
|Opción|Volver a generar la instancia de DAC|  
|------------|-------------------------------------|  
|Eliminar registro|Registre una DAC desde la base de datos que se ha mantenida en su lugar.|  
|Separar base de datos|Vuelva a adjuntar la base de datos usando **sp_attachdb** o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]y después registre una nueva instancia de DAC desde la base de datos.|  
|Eliminar base de datos|Restaure la base de datos a partir de una copia de seguridad completa realizada antes de que se eliminara la DAC, y, a continuación, registre una nueva instancia de la DAC a partir de la base de datos.|  
  
> [!WARNING]  
>  Recompilar una instancia de la DAC mediante el registro de una DAC desde una base de datos restaurada o adjuntada no volverá a crear algunas partes de la DAC original, como la directiva de selección de servidor.  
  
###  <a name="Permissions"></a> Permisos  
 Solo los miembros de los roles fijos de servidor **sysadmin** o **serveradmin** , o el propietario de la base de datos, pueden eliminar una DAC. La cuenta de administrador del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] integrada denominada **sa** también puede iniciar el asistente.  
  
##  <a name="UsingDeleteDACWizard"></a> Usar el asistente Eliminar aplicación de capa de datos  
 **Para eliminar una DAC mediante un asistente**  
  
1.  En **Explorador de objetos**, expanda el nodo de la instancia que contiene la DAC que se va a eliminar.  
  
2.  Expanda el nodo **Administración** .  
  
3.  Expanda el nodo **Aplicaciones de capa de datos** .  
  
4.  Haga clic con el botón derecho en la DAC que quiere eliminar y luego seleccione **Eliminar aplicación de capa de datos…**  
  
5.  Complete los cuadros de diálogo del asistente:  
  
    1.  [Introducción](#Introduction)  
  
    2.  [Elegir método](#Choose_method)  
  
    3.  [Resumen](#Summary)  
  
    4.  [Eliminar aplicación de capa de datos](#Delete_datatier_application)  
  
##  <a name="Introduction"></a> Página Introducción  
 Esta página describe los pasos para eliminar una aplicación de capa de datos.  
  
 **No volver a mostrar esta página.** - Haga clic en la casilla para evitar que la página se muestre en el futuro.  
  
 **Siguiente >**: continúa hasta la página **Elegir método**.  
  
 **Cancelar** : termina el asistente sin eliminar una aplicación de capa de datos o base de datos.  
  
 [Usar el asistente Eliminar aplicación de capa de datos](#UsingDeleteDACWizard)  
  
##  <a name="Choose_method"></a> Página Elegir método  
 Use esta página para especificar la opción a fin de controlar la base de datos asociada a la DAC que se va a eliminar.  
  
 **Eliminar registro** : quita los metadatos que definen la aplicación de capa de datos, pero deja intacta la base de datos asociada.  
  
 **Separar base de datos** : quita los metadatos que definen la aplicación de capa de datos y separa la base de datos asociada.  
  
 Esa instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)]no puede hacer referencia ya a la base de datos, pero los archivos de registro y de datos permanecen intactos.  
  
 **Eliminar base de datos** : quita los metadatos que definen la DAC y quita la base de datos asociada.  
  
 Los archivos de registro y de datos de la base de datos se eliminan de forma permanente.  
  
 **< Anterior**: vuelve a la página **Introducción**.  
  
 **Siguiente >**: avanza a la página **Resumen**.  
  
 **Cancelar** : termina el asistente sin eliminar la DAC o la base de datos.  
  
 [Usar el asistente Eliminar aplicación de capa de datos](#UsingDeleteDACWizard)  
  
##  <a name="Summary"></a> Página Resumen  
 Use esta página para revisar las acciones que el asistente realizará al eliminar la instancia de la DAC.  
  
 **Revisar opciones seleccionadas** : revise la DAC, la base de datos y el método de eliminación mostrados en el cuadro. Si la información es correcta, seleccione **Siguiente** o **Finalizar** para eliminar la DAC. Si la información de la base de datos y la DAC no es correcta, seleccione **Cancelar** y seleccione la DAC correcta. Si el método de eliminación no es correcto, seleccione **Anterior** para volver a la página **Elegir método** y seleccione un método diferente.  
  
 **< Anterior**: vuelve a la página **Elegir método** para elegir otro método de eliminación.  
  
 **Siguiente >**: elimina la instancia de DAC mediante el método elegido en la página anterior y avanza a la página **Eliminar aplicación de capa de datos**.  
  
 **Cancelar** : finaliza el asistente sin eliminar la instancia de DAC.  
  
 [Usar el asistente Eliminar aplicación de capa de datos](#UsingDeleteDACWizard)  
  
##  <a name="Delete_datatier_application"></a> Página Eliminar aplicación de capa de datos  
 Esta página notifica si la operación de eliminación se realizó correctamente o no.  
  
 **Eliminando la DAC** : notifica si cada acción realizada para eliminar la instancia de DAC se ha llevado a cabo correctamente o no. Revise la información para determinar si cada acción se realizó o no correctamente. Cualquier acción que encontrara un error tendrá un vínculo en la columna **Resultado** . Seleccione el vínculo para ver un informe del error para esa acción.  
  
 **Guardar informe** : seleccione este botón para guardar el informe de eliminación en un archivo HTML. El archivo notifica el estado de cada acción, incluidos todos los errores generados por cualquiera de las acciones. La carpeta predeterminada es una carpeta SQL Server Management Studio\DAC Packages de la carpeta Documentos de su cuenta de Windows.  
  
 **Finalizar** : termina el asistente.  
  
 [Usar el asistente Eliminar aplicación de capa de datos](#UsingDeleteDACWizard)  
  
##  <a name="DeleteDACPowerShell"></a> Eliminar una DAC mediante PowerShell  
 **Para eliminar una DAC mediante un script de PowerShell**  
  
1.  Cree un objeto SMO Server y establézcalo en la instancia que contiene la DAC que se va a eliminar.  
  
2.  Abra un objeto **ServerConnection** y conéctese a la misma instancia.  
  
3.  Use **add_DacActionStarted** y **add_DacActionFinished** para suscribirse a eventos de actualización de la DAC.  
  
4.  Especifique la DAC que desea eliminar.  
  
5.  Use uno de estos tres conjuntos de código, según la opción de eliminación que resulte apropiada:  
  
    -   Para eliminar el registro de la DAC, pero dejar la base de datos intacta, use el método **Unmanage()** .  
  
    -   Para eliminar el registro de la DAC y separar la base de datos, use el método **Uninstall()** y especifique **DetachDatabase**.  
  
    -   Para eliminar el registro de la DAC y quitar la base de datos, use el método **Uninstall()** y especifique **DropDatabase**.  
  
### <a name="example-deleting-the-dac-but-leaving-the-database-powershell"></a>Ejemplo para eliminar la DAC y mantener la base de datos (PowerShell)  
 En el ejemplo siguiente se elimina una DAC denominada MyApplication mediante el método **Unmanage()** para eliminar la DAC y dejar intacta la base de datos.  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Subscribe to the DAC delete events.  
$dacstore.add_DacActionStarted({Write-Host `n`nStarting at $(get-date) :: $_.Description})  
$dacstore.add_DacActionFinished({Write-Host Completed at $(get-date) :: $_.Description})  
  
## Specify the DAC to delete.  
$dacName  = "MyApplication"  
  
## Only delete the DAC definition from msdb, the associated database remains active.  
$dacstore.Unmanage($dacName)  
```  
  
 [Eliminar una DAC mediante PowerShell](#DeleteDACPowerShell)  
  
### <a name="example-deleting-the-dac-and-detaching-the-database-powershell"></a>Ejemplo para eliminar la DAC y separar la base de datos (PowerShell)  
 En el ejemplo siguiente se elimina una DAC denominada MyApplication mediante el método **Uninstall()** para eliminar la DAC y separar la base de datos.  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Subscribe to the DAC delete events.  
$dacstore.add_DacActionStarted({Write-Host `n`nStarting at $(get-date) :: $_.Description})  
$dacstore.add_DacActionFinished({Write-Host Completed at $(get-date) :: $_.Description})  
  
## Specify the DAC to delete.  
$dacName  = "MyApplication"  
  
## Delete the DAC definition from msdb and detach the associated database.  
$dacstore.Uninstall($dacName, [Microsoft.SqlServer.Management.Dac.DacUninstallMode]::DetachDatabase)  
```  
  
 [Eliminar una DAC mediante PowerShell](#DeleteDACPowerShell)  
  
### <a name="example-deleting-the-dac-and-dropping-the-database-powershell"></a>Ejemplo para eliminar la DAC y quitar la base de datos (PowerShell)  
 En el ejemplo siguiente se elimina una DAC denominada MyApplication mediante el método **Uninstall()** para eliminar la DAC y quitar la base de datos.  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Subscribe to the DAC delete events.  
$dacstore.add_DacActionStarted({Write-Host `n`nStarting at $(get-date) :: $_.Description})  
$dacstore.add_DacActionFinished({Write-Host Completed at $(get-date) :: $_.Description})  
  
## Specify the DAC to delete.  
$dacName  = "MyApplication"  
  
## Delete the DAC definition from msdb and drop the associated database.  
## $dacstore.Uninstall($dacName, [Microsoft.SqlServer.Management.Dac.DacUninstallMode]::DropDatabase)  
```  
  
 [Eliminar una DAC mediante PowerShell](#DeleteDACPowerShell)  
  
## <a name="see-also"></a>Vea también  
 [Aplicaciones de capa de datos](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [Aplicaciones de capa de datos](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [Implementar una aplicación de capa de datos](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)   
 [Registrar una base de datos como una DAC](../../relational-databases/data-tier-applications/register-a-database-as-a-dac.md)   
 [Realizar copias de seguridad y restaurar bases de datos de SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Adjuntar y separar bases de datos &#40;SQL Server&#41;](../../relational-databases/databases/database-detach-and-attach-sql-server.md)  
  
  

