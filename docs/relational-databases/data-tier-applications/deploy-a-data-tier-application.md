---
title: "Implementación una aplicación de capa de datos | Microsoft Docs"
ms.custom: 
ms.date: 01/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-data-tier-apps
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.swb.deploydacwizard.introduction.f1
- sql13.swb.deploydacwizard.deploydac.f1
- sql13.swb.deploydacwizard.summary.f1
- sql13.swb.deploydacwizard.updateconfiguration.f1
- sql13.swb.deploydacwizard.selectdac.f1
helpviewer_keywords:
- Deploy data-tier application
- deploy DAC
- data-tier application [SQL Server], deploy
- How to [DAC], deploy
- wizard [DAC], deploy
ms.assetid: c117af35-aa53-44a5-8034-fa8715dc735f
caps.latest.revision: "33"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 21bcace1cd6c05ac3516095aff955e24ff016967
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="deploy-a-data-tier-application"></a>Implementar una aplicación de capa de datos
  Implemente una aplicación de capa de datos (DAC) desde un paquete DAC en una instancia existente del motor de base de datos o de Azure SQL Database mediante un asistente o un script de PowerShell. 
  
 El proceso de implementación registra una instancia de DAC almacenando la definición de la DAC en la base de datos del sistema **msdb** (**maestra** en [!INCLUDE[ssSDS](../../includes/sssds-md.md)]), crea una base de datos y, después, rellena la base de datos con todos los objetos de base de datos definidos en la DAC.  
 
  
## <a name="deploy-the-same-dac-package-multiple-times"></a>Implementación del mismo paquete DAC varias veces 
 El mismo paquete DAC se puede implementar varias veces en una instancia única de [!INCLUDE[ssDE](../../includes/ssde-md.md)], sin embargo las implementaciones se deben ejecutar de una en una. El nombre de instancia de DAC que se especificó para cada implementación debe ser único en la instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
## <a name="managed-instances"></a>Instancias administradas  
 Si implementa una DAC en una instancia administrada del Motor de base de datos, la DAC implementada se incorpora a la **utilidad de SQL Server** la próxima vez que el conjunto de recopilación de utilidades se envíe desde la instancia al punto de control de la utilidad. Posteriormente, la DAC aparecerá en el nodo **Aplicaciones de capa de datos implementadas** del [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **Utility Explorer** and reported in the **Aplicaciones de capa de datos implementadas** details page.  
  
###  <a name="database-options-and-settings"></a>Opciones y configuración de bases de datos  
 De forma predeterminada, la base de datos que se cree durante la implementación incorporará toda la configuración predeterminada de la instrucción CREATE DATABASE, excepto en lo siguiente:  
  
-   La intercalación y nivel de compatibilidad de las bases de datos se establecen según los valores definidos en el paquete DAC. Un paquete DAC compilado a partir de un proyecto de base de datos en las Herramientas de Desarrollo de SQL Server usa los valores establecidos en el proyecto de base de datos. Un paquete que se haya extraído de una base de datos existente usará los valores de la base de datos original.  
  
-   Puede ajustar algunos de los valores de configuración de la base de datos, como por ejemplo el nombre de la base de datos y las rutas de archivo, en la página **Actualizar la configuración** . No puede establecer las rutas de acceso del archivo al realizar la implementación en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Algunas opciones de base de datos, como TRUSTWORTHY, DB_CHAINING y HONOR_BROKER_PRIORITY, no se pueden ajustar en el proceso de implementación. Las propiedades físicas, como el número de grupos de archivos o el número y tamaño de los archivos no se pueden modificar en el proceso de implementación. Una vez se haya completado la implementación, podrá usar la instrucción ALTER DATABASE, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell para personalizar la base de datos.  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 Una DAC puede implementarse en [!INCLUDE[ssSDS](../../includes/sssds-md.md)]o una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] que ejecute [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) o posterior. Si crea una DAC usando una versión posterior, la DAC puede contener objetos no admitidos por [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. No puede implementar dicha DAC en instancias de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
    
## <a name="security-and-permissions"></a>Seguridad y permisos
Los inicios de sesión de la autenticación están almacenados en un paquete DAC sin ninguna contraseña. Cuando el paquete se implementa o actualiza, el inicio de sesión se crea como un inicio de sesión deshabilitado con una contraseña generada. Para habilitar los inicios de sesión, use un inicio de sesión que disponga del permiso ALTER ANY LOGIN y emplee ALTER LOGIN para habilitar el inicio de sesión y asignar una nueva contraseña que pueda comunicar al usuario. Esto no se necesita para los inicios de sesión de Autenticación de Windows, porque SQL Server no administra sus contraseñas.  
  
 Una DAC solo la pueden implementar miembros de los roles fijos de servidor **sysadmin** o **serveradmin** , o los inicios de sesión que pertenezcan al rol fijo de servidor **dbcreator** y dispongan de permisos ALTER ANY LOGIN. La cuenta de administrador del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] integrada denominada **sa** también puede implementar una DAC. 

Al implementar una DAC con inicios de sesión en [!INCLUDE[ssSDS](../../includes/sssds-md.md)] , se requiere la pertenencia a los roles loginmanager o serveradmin. La implementación de una DAC sin inicios de sesión en [!INCLUDE[ssSDS](../../includes/sssds-md.md)] necesita la pertenencia a los roles dbmanager o serveradmin.  
  
## <a name="deploy-a-dac-using-the-wizard"></a>Implementación de una DAC mediante un asistente  
  
1.  En el **Explorador de objetos**, expanda el nodo de la instancia en la que desee implementar la DAC.  
  
2.  Haga clic con el botón derecho en el nodo **Bases de datos** y seleccione **Implementar aplicación de capa de datos…**  
  
3.  Finalice los cuadros de diálogo del Asistente y haga clic en Finalizar.
Más información sobre algunas de las páginas del asistente: 
     
### <a name="select-dac-package-page"></a>Página Seleccionar paquete DAC  
 Especifique el paquete DAC que contiene la aplicación de capa de datos que se va a implementar. La página pasa por tres estados.  
    
### <a name="select-the-dac-package"></a>Seleccionar el paquete DAC  
 Seleccionar el paquete DAC que desee implementar El paquete DAC debe ser un archivo de paquete DAC válido y tener una extensión .dacpac.  
  
 **Paquete DAC:** especifique la ruta de acceso y el nombre del archivo del paquete DAC que contiene la aplicación de capa de datos que se va a implementar. Puede seleccionar el botón **Examinar** a la derecha del cuadro para ir a la ubicación del paquete DAC.  
  
 **Nombre de aplicación:** cuadro de solo lectura que muestra el nombre de DAC que se asignó cuando la DAC se creó o extrajo de una base de datos.  
  
 **Versión:** cuadro de solo lectura que muestra la versión que se asignó cuando la DAC se creó o extrajo de una base de datos.  
  
 **Descripción:** cuadro de solo lectura que muestra la descripción que se escribió cuando la DAC se creó o extrajo de una base de datos.  
  
### <a name="validating-the-dac-package"></a>Validar el paquete DAC  
 Muestra una barra de progreso cuando el asistente confirma que el archivo seleccionado es un paquete DAC válido. Si se valida el paquete DAC, el asistente pasa a la versión final de la página **Seleccionar paquete** , donde podrá comprobar los resultados de la validación. Si el archivo no es un paquete DAC válido, el asistente se queda en **Seleccionar paquete DAC**. Seleccione otro paquete DAC válido o cancele el asistente y genere un nuevo paquete DAC.  
  
  ### <a name="review-policy-page"></a>Página Revisar directiva  
 Revise los resultados de la evaluación de la directiva de selección de servidores de DAC (en caso de que se utilice). La directiva de selección de servidores de DAC es opcional y está asignada a la DAC cuando se crea en Visual Studio. La directiva se sirve de las facetas de la directiva de selección de servidores para especificar las condiciones que debe cumplir una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] para hospedar la DAC.  
  
 **Resultados de evaluación de condiciones de directivas**: muestra si se han cumplido correctamente las condiciones de la directiva de implementación de DAC. Los resultados de la evaluación de cada condición se notifican en una línea independiente.  
  
 Las siguientes directivas de selección de servidor siempre se evalúan como falsas al implementar una DAC en [!INCLUDE[ssSDS](../../includes/sssds-md.md)]: la versión del sistema operativo, el lenguaje, las canalizaciones con nombre habilitadas, las plataforma y tcp habilitado.  
  
 **Pasar por alto infracciones de directivas:** use esta casilla para comenzar con la implementación si se produce un error en una o más de las condiciones de la directiva. Seleccione esta opción solamente si está seguro de que todas las condiciones que produjeron errores no evitarán la correcta operación de la DAC.  
   
### <a name="update-configuration-page"></a>Página Actualizar la configuración  
 Especifique los nombres de la instancia de DAC implementada y la base de datos que ha creado la implementación, así como para establecer las opciones de base de datos.  
  
 **Nombre de la base de datos:** especifica el nombre de la base de datos que se creará en la implementación. El valor predeterminado es el nombre de la base de datos de origen de donde se extrajo la DAC. El nombre debe ser único en la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] y cumplir las reglas de los identificadores de [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
 Si cambia el nombre de la base de datos, los nombres de los archivos de datos y de registro cambiarán para coincidir con el nuevo valor.  
  
 El nombre de la base de datos también se utiliza como nombre de la instancia de DAC. El nombre de instancia se muestra en el nodo para la DAC en el nodo **Aplicaciones de capa de datos** en **Explorador de objetos**, o bien en el nodo **Aplicaciones de capa de datos implementadas** en el **Explorador de la utilidad**.  
  
 Las siguientes opciones no se aplican a [!INCLUDE[ssSDS](../../includes/sssds-md.md)]y no se muestran al realizar la implementación en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 **Utilizar la ubicación de base de datos predeterminada:** seleccione esta opción para crear los archivos de datos de la base de datos y los archivos de registro en la ubicación predeterminada para la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Los nombres de archivo se generarán utilizando el nombre de la base de datos.  
  
 **Especificar archivos de base de datos:** seleccione esta opción para especificar una ubicación o un nombre diferentes para los archivos de datos y de registro.  
  
 **Ruta de acceso y nombre del archivo de datos:** especifique la ruta completa y el nombre de archivo del archivo de datos. El cuadro se rellena con la ruta de acceso y nombre de archivo predeterminados. Modifique la cadena en el cuadro para cambiar el valor predeterminado o utilice el botón Examinar para navegar hasta la carpeta donde el archivo de datos se va a colocar.  
  
 **Ruta de acceso y nombre del archivo de registro:** especifique la ruta de acceso completa y el nombre de archivo del archivo de registro. El cuadro se rellena con la ruta de acceso y nombre de archivo predeterminados. Modifique la cadena en el cuadro para cambiar el valor predeterminado o utilice el botón **Examinar** para navegar hasta la carpeta donde se va a colocar el archivo de registro.  
  
###  <a name="Summary"></a> Página Resumen  
 Use esta página para comprobar las acciones que el asistente realizará al implementar la DAC.  
  
 **La siguiente configuración se utilizará en la implementación de su DAC.** - Compruebe la información que se muestra para asegurarse de que las acciones emprenda serán las correctas. La ventana muestra el paquete DAC y el nombre que seleccionó para la instancia de DAC implementada. La ventana también muestra los valores de configuración que se utilizarán al crear la base de datos asociada con la DAC.  
   
### <a name="deploy-page"></a>Página Implementar  
 Esta página notifica si la operación de implementación se realizó correctamente o no.  
  
 **Implementación de DAC:** notifica si cada acción realizada para implementar la DAC se realizó o no correctamente. Revise la información para determinar si cada acción se realizó o no correctamente. Cualquier acción que encontrara un error tendrá un vínculo en la columna **Resultado** . Seleccione el vínculo para ver un informe del error para esa acción.  
  
 **Guardar informe:** seleccione este botón para guardar el informe de implementación en un archivo HTML. El archivo notifica el estado de cada acción, incluidos todos los errores generados por cualquiera de las acciones. La carpeta predeterminada es la carpeta SQL Server Management Studio\DAC Packages de la carpeta Documentos de su cuenta de Windows.  
  
  
##  <a name="deploy-a-dac-using-powershell"></a>Implementación de una DAC mediante PowerShell  
  
1.  Cree un objeto SMO Server y establézcalo en la instancia en la que desea implementar la DAC.  
  
2.  Abra un objeto **ServerConnection** y conéctese a la misma instancia.  
  
3.  Use **System.IO.File** para cargar el archivo de paquete DAC.  
  
4.  Use **add_DacActionStarted** y **add_DacActionFinished** para suscribirse a los eventos de implementación de la DAC.  
  
5.  Establezca **DatabaseDeploymentProperties**.  
  
6.  Use el método **DacStore.Install** para implementar la DAC.  
  
7.  Cierra la secuencia de archivos usada para leer el archivo de paquete DAC.  
  
## <a name="powershell-examples"></a>Ejemplos de PowerShell  
 En el siguiente ejemplo se implementa la DAC denominada MyApplication en una instancia predeterminada de [!INCLUDE[ssDE](../../includes/ssde-md.md)], mediante una definición de DAC de un paquete de MyApplication.dacpac.  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Load the DAC package file.  
$dacpacPath = "C:\MyDACs\MyApplication.dacpac"  
$fileStream = [System.IO.File]::Open($dacpacPath,[System.IO.FileMode]::OpenOrCreate)  
$dacType = [Microsoft.SqlServer.Management.Dac.DacType]::Load($fileStream)  
  
## Subscribe to the DAC deployment events.  
$dacstore.add_DacActionStarted({Write-Host `n`nStarting at $(get-date) :: $_.Description})  
$dacstore.add_DacActionFinished({Write-Host Completed at $(get-date) :: $_.Description})  
  
## Deploy the DAC and create the database.  
$dacName  = "MyApplication"  
$evaluateTSPolicy = $true  
$deployProperties = New-Object Microsoft.SqlServer.Management.Dac.DatabaseDeploymentProperties($serverconnection,$dacName)  
$dacstore.Install($dacType, $deployProperties, $evaluateTSPolicy)  
$fileStream.Close()  
```  
  
## <a name="more-information"></a>Más información 
 [Aplicaciones de capa de datos](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [Extraer una DAC de una base de datos](../../relational-databases/data-tier-applications/extract-a-dac-from-a-database.md)   
 [Identificadores de base de datos](../../relational-databases/databases/database-identifiers.md)  
  
  
