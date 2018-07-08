---
title: Implementación una aplicación de capa de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-data-tier-apps
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.deploydacwizard.updateconfiguration.f1
- sql12.swb.deploydacwizard.selectdac.f1
- sql12.swb.deploydacwizard.deploydac.f1
- sql12.swb.deploydacwizard.introduction.f1
- sql12.swb.deploydacwizard.summary.f1
helpviewer_keywords:
- Deploy data-tier application
- deploy DAC
- data-tier application [SQL Server], deploy
- How to [DAC], deploy
- wizard [DAC], deploy
ms.assetid: c117af35-aa53-44a5-8034-fa8715dc735f
caps.latest.revision: 31
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7041a4e15314f7efa8ea626e41ed705b69faa18c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37154536"
---
# <a name="deploy-a-data-tier-application"></a>Implementar una aplicación de capa de datos
  Puede implementar una aplicación de capa de datos (DAC) desde un paquete DAC en una instancia existente del [!INCLUDE[ssDE](../../includes/ssde-md.md)] o de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] mediante un asistente o un script de PowerShell. El proceso de implementación registra una instancia de DAC almacenando la definición de la DAC en la base de datos del sistema **msdb** (**maestra** en [!INCLUDE[ssSDS](../../includes/sssds-md.md)]), crea una base de datos y, después, rellena la base de datos con todos los objetos de base de datos definidos en la DAC.  
  
-   **Antes de empezar:**  [Utilidad de SQL Server](#SQLUtility), [Opciones y configuración de bases de datos](#DBOptSettings), [Limitaciones y restricciones](#LimitationsRestrictions), [Requisitos previos](#Prerequisites), [Seguridad](#Security), [Permisos](#Permissions)  
  
-   **Para implementar una DAC con:**  [Asistente Implementar aplicación de capa de datos](#UsingDeployDACWizard), [PowerShell](#DeployDACPowerShell)  
  
##  <a name="BeforeBegin"></a> Antes de empezar  
 El mismo paquete DAC se puede implementar varias veces en una instancia única de [!INCLUDE[ssDE](../../includes/ssde-md.md)] , sin embargo las implementaciones se deben ejecutar de una en una. El nombre de instancia de DAC que se especificó para cada implementación debe ser único en la instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
###  <a name="SQLUtility"></a> Utilidad de SQL Server  
 Si implementa una DAC en una instancia administrada del Motor de base de datos, la DAC implementada se incorpora a la Utilidad de SQL Server la próxima vez que el conjunto de recopilación de utilidades se envíe desde la instancia al punto de control de la utilidad. Posteriormente, la DAC aparecerá en el nodo **Aplicaciones de capa de datos implementadas** del [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **Utility Explorer** and reported in the **Aplicaciones de capa de datos implementadas** details page.  
  
###  <a name="DBOptSettings"></a> Opciones y configuración de bases de datos  
 De forma predeterminada, la base de datos que se cree durante la implementación incorporará toda la configuración predeterminada de la instrucción CREATE DATABASE, excepto en lo siguiente:  
  
-   La intercalación y nivel de compatibilidad de las bases de datos se establecen según los valores definidos en el paquete DAC. Un paquete DAC compilado a partir de un proyecto de base de datos en las Herramientas de Desarrollo de SQL Server usa los valores establecidos en el proyecto de base de datos. Un paquete que se haya extraído de una base de datos existente usará los valores de la base de datos original.  
  
-   Puede ajustar algunos de los valores de configuración de la base de datos, como por ejemplo el nombre de la base de datos y las rutas de archivo, en la página **Actualizar la configuración** . No puede establecer las rutas de acceso del archivo al realizar la implementación en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Algunas opciones de base de datos, como TRUSTWORTHY, DB_CHAINING y HONOR_BROKER_PRIORITY, no se pueden ajustar en el proceso de implementación. Las propiedades físicas, como el número de grupos de archivos o el número y tamaño de los archivos no se pueden modificar en el proceso de implementación. Una vez se haya completado la implementación, podrá usar la instrucción ALTER DATABASE, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell para personalizar la base de datos.  
  
###  <a name="LimitationsRestrictions"></a> Limitaciones y restricciones  
 Una DAC puede implementarse en [!INCLUDE[ssSDS](../../includes/sssds-md.md)]o una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] que ejecute [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) o posterior. Si crea una DAC usando una versión posterior, la DAC puede contener objetos no admitidos por [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. No puede implementar dicha DAC en instancias de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
###  <a name="Prerequisites"></a> Requisitos previos  
 Se recomienda no implementar un paquete DAC desde orígenes desconocidos o que no sean de confianza. Es posible que estos paquetes contengan código malintencionado que podría ejecutar código Transact-SQL no deseado o provocar errores al modificar el esquema o la estructura de la base de datos física. Antes de usar un paquete desde un origen desconocido o que no sea de confianza, desempaquete la DAC y examine el código, como por ejemplo procedimientos almacenados u otro código definido por el usuario. Para más información sobre cómo realizar estas comprobaciones, consulte [Validar un paquete de DAC](validate-a-dac-package.md).  
  
###  <a name="Security"></a> Seguridad  
 Para mejorar la seguridad, los inicios de sesión de la autenticación de SQL Server están almacenados en un paquete DAC sin ninguna contraseña. Cuando el paquete se implementa o actualiza, el inicio de sesión se crea como un inicio de sesión deshabilitado con una contraseña generada. Para habilitar los inicios de sesión, use un inicio de sesión que disponga del permiso ALTER ANY LOGIN y emplee ALTER LOGIN para habilitar el inicio de sesión y asignar una nueva contraseña que pueda comunicar al usuario. Esto no se necesita para los inicios de sesión de Autenticación de Windows, porque SQL Server no administra sus contraseñas.  
  
####  <a name="Permissions"></a> Permissions  
 Una DAC solo la pueden implementar miembros de los roles fijos de servidor **sysadmin** o **serveradmin** , o los inicios de sesión que pertenezcan al rol fijo de servidor **dbcreator** y dispongan de permisos ALTER ANY LOGIN. La cuenta de administrador del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] integrada denominada **sa** también puede implementar una DAC. Al implementar una DAC con inicios de sesión en [!INCLUDE[ssSDS](../../includes/sssds-md.md)] , se requiere la pertenencia a los roles loginmanager o serveradmin. La implementación de una DAC sin inicios de sesión en [!INCLUDE[ssSDS](../../includes/sssds-md.md)] necesita la pertenencia a los roles dbmanager o serveradmin.  
  
##  <a name="UsingDeployDACWizard"></a> Mediante el Asistente para aplicaciones de capa de datos de implementación  
 **Para implementar una DAC mediante un asistente**  
  
1.  En el **Explorador de objetos**, expanda el nodo de la instancia en la que desee implementar la DAC.  
  
2.  Haga clic con el botón derecho en el nodo **Bases de datos** y seleccione **Implementar aplicación de capa de datos…**  
  
3.  Complete los cuadros de diálogo del asistente:  
  
    -   [Página Introducción](#Introduction)  
  
    -   [Página Seleccionar paquete DAC](#Select_dac_package)  
  
    -   [Página Revisar directiva](#Review_policy)  
  
    -   [Página Actualizar la configuración](#Update_configuration)  
  
    -   [Página Resumen](#Summary)  
  
    -   [Página implementar](#Deploy)  
  
##  <a name="Introduction"></a> Página Introducción  
 Esta página describe los pasos para implementar una aplicación de capa de datos.  
  
 **No volver a mostrar esta página.** - Haga clic en la casilla para evitar que la página se muestre en el futuro.  
  
 **Siguiente >:** avanza a la página **Seleccionar paquete DAC**.  
  
 **Cancelar:** termina el asistente sin implementar una DAC.  
  
##  <a name="Select_dac_package"></a> Página Seleccionar paquete DAC  
 Use esta página para especificar el paquete DAC que contiene la aplicación de capa de datos que se va a implementar. La página pasa por tres estados.  
  
### <a name="select-the-dac-package"></a>Seleccionar el paquete DAC  
 Use el estado inicial de la página para elegir el paquete DAC que se va a implementar. El paquete DAC debe ser un archivo de paquete DAC válido y tener una extensión .dacpac.  
  
 **Paquete DAC:** especifique la ruta de acceso y el nombre del archivo del paquete DAC que contiene la aplicación de capa de datos que se va a implementar. Puede seleccionar el botón **Examinar** a la derecha del cuadro para ir a la ubicación del paquete DAC.  
  
 **Nombre de aplicación:** cuadro de solo lectura que muestra el nombre de DAC que se asignó cuando la DAC se creó o extrajo de una base de datos.  
  
 **Versión:** cuadro de solo lectura que muestra la versión que se asignó cuando la DAC se creó o extrajo de una base de datos.  
  
 **Descripción:** cuadro de solo lectura que muestra la descripción que se escribió cuando la DAC se creó o extrajo de una base de datos.  
  
 **\< Anterior** : vuelve a la página **Introducción** .  
  
 **Siguiente>:** muestra una barra de progreso cuando el asistente confirma que el archivo seleccionado es un paquete DAC válido.  
  
 **Cancelar:** termina el asistente sin implementar la DAC.  
  
### <a name="validating-the-dac-package"></a>Validar el paquete DAC  
 Muestra una barra de progreso cuando el asistente confirma que el archivo seleccionado es un paquete DAC válido. Si se valida el paquete DAC, el asistente pasa a la versión final de la página **Seleccionar paquete** , donde podrá comprobar los resultados de la validación. Si el archivo no es un paquete DAC válido, el asistente se queda en **Seleccionar paquete DAC**. Seleccione otro paquete DAC válido o cancele el asistente y genere un nuevo paquete DAC.  
  
 **Validando el contenido de DAC:** barra de progreso que notifica el estado actual del proceso de validación.  
  
 **\< Anterior** -vuelve al estado inicial de la **Seleccionar paquete** página.  
  
 **Siguiente>:** avanza a la versión final de la página **Seleccionar paquete**.  
  
 **Cancelar:** termina el asistente sin implementar la DAC.  
  
##  <a name="Review_policy"></a> Página Revisar directiva  
 Use esta página para revisar los resultados de la evaluación de la directiva de selección de servidores de DAC, en caso de que la DAC tenga una directiva. La directiva de selección de servidores de DAC es opcional y está asignada a la DAC cuando se crea en Visual Studio. La directiva se sirve de las facetas de la directiva de selección de servidores para especificar las condiciones que debe cumplir una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] para hospedar la DAC.  
  
 **Resultados de evaluación de condiciones de directivas:** informe de solo lectura que muestra si se han cumplido correctamente las condiciones de la directiva de implementación de DAC. Los resultados de la evaluación de cada condición se notifican en una línea independiente.  
  
 Las siguientes directivas de selección de servidor siempre se evalúan como falsas al implementar una DAC en [!INCLUDE[ssSDS](../../includes/sssds-md.md)]: la versión del sistema operativo, el lenguaje, las canalizaciones con nombre habilitadas, las plataforma y tcp habilitado.  
  
 **Pasar por alto infracciones de directivas:** use esta casilla para comenzar con la implementación si se produce un error en una o más de las condiciones de la directiva. Seleccione esta opción solamente si está seguro de que todas las condiciones que produjeron errores no evitarán la correcta operación de la DAC.  
  
 **\< Anterior** -devuelve a la **Seleccionar paquete** página.  
  
 **Siguiente>:** avanza a la página **Actualizar la configuración**.  
  
 **Cancelar:** termina el asistente sin implementar la DAC.  
  
##  <a name="Update_configuration"></a> Página Actualizar la configuración  
 Use esta página para especificar los nombres de la instancia de DAC implementada y la base de datos que ha creado la implementación, así como para establecer las opciones de base de datos.  
  
 **Nombre de la base de datos:** especifica el nombre de la base de datos que se creará en la implementación. El valor predeterminado es el nombre de la base de datos de origen de donde se extrajo la DAC. El nombre debe ser único en la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] y cumplir las reglas de los identificadores de [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
 Si cambia el nombre de la base de datos, los nombres de los archivos de datos y de registro cambiarán para coincidir con el nuevo valor.  
  
 El nombre de la base de datos también se utiliza como nombre de la instancia de DAC. El nombre de instancia se muestra en el nodo para la DAC en el nodo **Aplicaciones de capa de datos** en **Explorador de objetos**, o bien en el nodo **Aplicaciones de capa de datos implementadas** en el **Explorador de la utilidad**.  
  
 Las siguientes opciones no se aplican a [!INCLUDE[ssSDS](../../includes/sssds-md.md)]y no se muestran al realizar la implementación en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 **Utilizar la ubicación de base de datos predeterminada:** seleccione esta opción para crear los archivos de datos de la base de datos y los archivos de registro en la ubicación predeterminada para la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Los nombres de archivo se generarán utilizando el nombre de la base de datos.  
  
 **Especificar archivos de base de datos:** seleccione esta opción para especificar una ubicación o un nombre diferentes para los archivos de datos y de registro.  
  
 **Ruta de acceso y nombre del archivo de datos:** especifique la ruta completa y el nombre de archivo del archivo de datos. El cuadro se rellena con la ruta de acceso y nombre de archivo predeterminados. Modifique la cadena en el cuadro para cambiar el valor predeterminado o utilice el botón Examinar para navegar hasta la carpeta donde el archivo de datos se va a colocar.  
  
 **Ruta de acceso y nombre del archivo de registro:** especifique la ruta de acceso completa y el nombre de archivo del archivo de registro. El cuadro se rellena con la ruta de acceso y nombre de archivo predeterminados. Modifique la cadena en el cuadro para cambiar el valor predeterminado o utilice el botón **Examinar** para navegar hasta la carpeta donde se va a colocar el archivo de registro.  
  
 **\< Anterior** -devuelve a la **Seleccionar paquete DAC** página.  
  
 **Siguiente >**: avanza a la página **Resumen**.  
  
 **Cancelar:** termina el asistente sin implementar la DAC.  
  
##  <a name="Summary"></a> Página Resumen  
 Use esta página para comprobar las acciones que el asistente realizará al implementar la DAC.  
  
 **La siguiente configuración se utilizará en la implementación de su DAC.** - Compruebe la información que se muestra para asegurarse de que las acciones emprenda serán las correctas. La ventana muestra el paquete DAC y el nombre que seleccionó para la instancia de DAC implementada. La ventana también muestra los valores de configuración que se utilizarán al crear la base de datos asociada con la DAC.  
  
 **\< Anterior** -vuelve a la **actualizar la configuración** página para cambiar sus selecciones.  
  
 **Siguiente >**: implementa la DAC y muestra los resultados en la página **Implementar DAC**.  
  
 **Cancelar:** termina el asistente sin implementar la DAC.  
  
##  <a name="Deploy"></a> Página implementar  
 Esta página notifica si la operación de implementación se realizó correctamente o no.  
  
 **Implementación de DAC:** notifica si cada acción realizada para implementar la DAC se realizó o no correctamente. Revise la información para determinar si cada acción se realizó o no correctamente. Cualquier acción que encontrara un error tendrá un vínculo en la columna **Resultado** . Seleccione el vínculo para ver un informe del error para esa acción.  
  
 **Guardar informe:** seleccione este botón para guardar el informe de implementación en un archivo HTML. El archivo notifica el estado de cada acción, incluidos todos los errores generados por cualquiera de las acciones. La carpeta predeterminada es la carpeta SQL Server Management Studio\DAC Packages de la carpeta Documentos de su cuenta de Windows.  
  
 **Finalizar** : termina el asistente.  
  
##  <a name="DeployDACPowerShell"></a> Usar PowerShell  
 **Para implementar una DAC mediante el método Install() en un script de PowerShell**  
  
1.  Cree un objeto SMO Server y establézcalo en la instancia en la que desea implementar la DAC.  
  
2.  Abra un `ServerConnection` de objetos y conectarse a la misma instancia.  
  
3.  Use `System.IO.File` para cargar el archivo de paquete DAC.  
  
4.  Use `add_DacActionStarted` y `add_DacActionFinished` para suscribirse a los eventos de implementación de DAC.  
  
5.  Establecer el `DatabaseDeploymentProperties`.  
  
6.  Use el método `DacStore.Install` para implementar la DAC.  
  
7.  Cierra la secuencia de archivos usada para leer el archivo de paquete DAC.  
  
### <a name="example-powershell"></a>Ejemplo (PowerShell)  
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
  
## <a name="see-also"></a>Vea también  
 [Aplicaciones de capa de datos](data-tier-applications.md)   
 [Extraer una DAC de una base de datos](extract-a-dac-from-a-database.md)   
 [Identificadores de base de datos](../databases/database-identifiers.md)  
  
  
