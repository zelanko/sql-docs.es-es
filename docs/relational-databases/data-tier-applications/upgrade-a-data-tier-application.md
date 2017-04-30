---
title: "Actualizar una aplicación de capa de datos | Microsoft Docs"
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
- sql13.swb.upgradedacwizard.summary.f1
- sql13.swb.upgradedacwizard.reviewplan.f1
- sql13.swb.upgradedacwizard.upgradedac.f1
- sql13.swb.upgradedacwizard.selectpackage.f1
- sql13.swb.upgradedacwizard.reviewpolicy.f1
- sql13.swb.upgradedacwizard.selectoptions.f1
- sql13.swb.upgradedacwizard.checkdrift.f1
- sql13.swb.upgradedacwizard.introduction.f1
helpviewer_keywords:
- upgrade DAC
- data-tier application [SQL Server], upgrade
- wizard [DAC], upgrade
- How to [DAC], upgrade
ms.assetid: c117df94-f02b-403f-9383-ec5b3ac3763c
caps.latest.revision: 35
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7989f6c7fa8ff85ceb5cb5ed06d989343edb46a2
ms.lasthandoff: 04/11/2017

---
# <a name="upgrade-a-data-tier-application"></a>Actualizar una aplicación de capa de datos
  Use el Asistente Actualizar aplicación de capa de datos o un script de Windows PowerShell para cambiar el esquema y las propiedades de una aplicación de capa de datos (DAC) implementada actualmente para coincidir con el esquema y las propiedades definidas en una versión nueva de la DAC.  
  
-   **Before you begin:**  [Choosing DAC Upgrade Options](#ChoseDACUpgOptions), [Limitations and Restrictions](#LimitationsRestrictions), [Prerequisites](#Prerequisites), [Security](#Security), [Permissions](#Permissions)  
  
-   **To upgrade a DAC, using:**  [The Upgrade Data-tier Application Wizard](#UsingDACUpgradeWizard), [PowerShell](#UpgradeDACPowerShell)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
 Una actualización de DAC es un proceso en contexto que modifica el esquema de la base de datos existente para coincidir con el esquema definido en una nueva versión de la DAC. La nueva versión de la DAC se proporciona en un archivo de paquete DAC. Para obtener más información sobre cómo crear un paquete DAC, vea [Aplicaciones de capa de datos](../../relational-databases/data-tier-applications/data-tier-applications.md).  
  
###  <a name="ChoseDACUpgOptions"></a> Elegir opciones de actualización de DAC  
 Hay cuatro opciones de actualización para una actualización en contexto:  
  
-   **Ignorar la pérdida de datos** : si es **True**, la actualización continuará incluso si alguna de las operaciones provocan la pérdida de datos. Si es **False**, estas operaciones terminarán la actualización. Por ejemplo, si no hay una tabla de la base de datos actual en el esquema de la nueva DAC, la tabla se quitará si se especifica **True** . El valor predeterminado es **True**.  
  
-   **Bloquear si hay cambios** : si es **True**, la actualización se termina si el esquema de la base de datos es diferente al definido en la DAC anterior. Si es **False**, la actualización continúa incluso si se detectan cambios. El valor predeterminado es **False**.  
  
-   **Revertir si hay error** : si es **True**, la actualización se incluye en una transacción y, si se encuentran errores, se intenta revertir. Si es **False**, se confirman todos los cambios a medida que se efectúan y, si se producen errores, puede que tenga que restaurar una copia de seguridad anterior de la base de datos. El valor predeterminado es **False**.  
  
-   **Omitir validación de directiva** : si es **True**, la directiva de selección del servidor DAC no se evalúa. Si es **False**, se evalúa la directiva y la actualización se termina si se produce un error en la validación. El valor predeterminado es **False**.  
  
###  <a name="LimitationsRestrictions"></a> Limitaciones y restricciones  
 Las actualizaciones de DAC solo se pueden realizar en [!INCLUDE[ssSDS](../../includes/sssds-md.md)]o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) o posterior.  
  
###  <a name="Prerequisites"></a> Requisitos previos  
 Es conveniente hacer una copia de seguridad completa de la base de datos antes de comenzar la actualización. Si una actualización encuentra un error y no puede revertir todos sus cambios, puede que tenga que restaurar la copia de seguridad.  
  
 Antes de iniciar la actualización, hay varias acciones que debe realizar para validar el paquete DAC y las acciones de actualización. Para obtener más información acerca de cómo realizar estas comprobaciones, vea [Validate a DAC Package](../../relational-databases/data-tier-applications/validate-a-dac-package.md).  
  
-   Recomendamos no realizar la actualización con un paquete DAC de fuentes desconocidas o que no sean de confianza. Es posible que estos paquetes contengan código malintencionado que podría ejecutar código Transact-SQL no deseado o provocar errores al modificar el esquema o la estructura de la base de datos física. Antes de usar un paquete desde un origen desconocido o que no sea de confianza, desempaquete la DAC y examine el código, como por ejemplo procedimientos almacenados u otro código definido por el usuario.  
  
-   Si se han realizado cambios en la base de datos actual tras la implementación de la última versión de la DAC, algunos de los cambios pueden impedir que la actualización se complete correctamente o puede que la actualización los quite. Primero debe generar y revisar un informe de los cambios efectuados en la base de datos.  
  
-   Es conveniente generar una lista de los cambios en el esquema que va a realizar la actualización y revisar la lista para comprobar si existe algún problema.  
  
 El nombre de la aplicación en el paquete DAC debe coincidir con el nombre de la aplicación de la DAC implementada actualmente. Por ejemplo, si la DAC actual tiene un nombre de aplicación **GeneralLedger**, solo se puede actualizar mediante un paquete DAC que tenga también un nombre de aplicación **GeneralLedger**.  
  
 Asegúrese de que hay suficiente espacio del registro de transacciones disponible para registrar todas las modificaciones.  
  
###  <a name="Security"></a> Seguridad  
 Para mejorar la seguridad, los inicios de sesión de la autenticación de SQL Server están almacenados en un paquete DAC sin ninguna contraseña. Cuando el paquete se implementa o actualiza, el inicio de sesión se crea como un inicio de sesión deshabilitado con una contraseña generada. Para habilitar los inicios de sesión, use un inicio de sesión que disponga del permiso ALTER ANY LOGIN y emplee ALTER LOGIN para habilitar el inicio de sesión y asignar una nueva contraseña que pueda comunicar al usuario. Esto no se necesita para los inicios de sesión de Autenticación de Windows, porque SQL Server no administra sus contraseñas.  
  
####  <a name="Permissions"></a> Permisos  
 Una DAC solo la pueden actualizar miembros de los roles fijos de servidor **sysadmin** o **serveradmin** , o los inicios de sesión que pertenezcan al rol fijo de servidor **dbcreator** y dispongan de permisos ALTER ANY LOGIN. El inicio de sesión debe ser el propietario de la base de datos existente. La cuenta de administrador del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] integrada denominada **sa** también puede actualizar una DAC.  
  
##  <a name="UsingDACUpgradeWizard"></a> Usar el Asistente Actualizar aplicación de capa de datos  
 **Para actualizar una DAC mediante un asistente**  
  
1.  En **Explorador de objetos**, expanda el nodo de la instancia que contiene la DAC que se va a actualizar.  
  
2.  Expanda el nodo **Administración** y, después, expanda el nodo **Aplicaciones de capa de datos** .  
  
3.  Haga clic con el botón derecho en el nodo de la DAC que se actualizará y, luego, seleccione **Actualizar aplicación de capa de datos…**.  
  
4.  Complete los cuadros de diálogo del asistente:  
  
    1.  [Página Introducción](#Introduction)  
  
    2.  [Página Seleccionar paquete](#Select_dac_package)  
  
    3.  [Página Revisar directiva](#Review_policy)  
  
    4.  [Página Detectar cambio](#Detect_change)  
  
    5.  [Revisar el plan de actualización](#ReviewUpgPlan)  
  
    6.  [Página Resumen](#Summary)  
  
    7.  [Página Actualizar DAC](#Upgrade)  
  
##  <a name="Introduction"></a> Página Introducción  
 Esta página describe los pasos para actualizar una aplicación de capa de datos.  
  
 **No volver a mostrar esta página.** - Haga clic en la casilla para evitar que la página se muestre en el futuro.  
  
 **Siguiente >:** avanza a la página **Seleccionar paquete**.  
  
 **Cancelar:** termina el asistente sin actualizar la DAC.  
  
##  <a name="Select_dac_package"></a> Página Seleccionar paquete  
 Use esta página para especificar el paquete DAC que contiene la nueva versión de la aplicación de capa de datos. Las página pasa por dos estados.  
  
### <a name="select-the-dac-package"></a>Seleccionar el paquete DAC  
 Use el estado inicial de la página para elegir el paquete DAC que se va a implementar. El paquete DAC debe ser un archivo de paquete DAC válido y tener una extensión .dacpac. El nombre de la aplicación DAC en el paquete DAC debe ser el mismo que el de la aplicación de la DAC actual.  
  
 **Paquete DAC:** especifique la ruta de acceso y el nombre del archivo del paquete DAC que contiene la nueva versión de la aplicación de capa de datos. Puede seleccionar el botón **Examinar** a la derecha del cuadro para ir a la ubicación del paquete DAC.  
  
 **Nombre de aplicación:** cuadro de solo lectura que muestra el nombre de la aplicación DAC que se asignó cuando la DAC se creó o extrajo de una base de datos.  
  
 **Versión:** cuadro de solo lectura que muestra la versión que se asignó cuando la DAC se creó o extrajo de una base de datos.  
  
 **Descripción:** cuadro de solo lectura que muestra la descripción que se escribió cuando la DAC se creó o extrajo de una base de datos.  
  
 **< Anterior:** vuelve a la página **Introducción**.  
  
 **Siguiente>:** muestra una barra de progreso cuando el asistente confirma que el archivo seleccionado es un paquete DAC válido.  
  
 **Cancelar:** termina el asistente sin actualizar la DAC.  
  
### <a name="validating-the-dac-package"></a>Validar el paquete DAC  
 Muestra una barra de progreso cuando el asistente confirma que el archivo seleccionado es un paquete DAC válido. Si se valida el paquete DAC, el asistente va a la página **Revisar directiva** . Si el archivo no es un paquete DAC válido, el asistente se queda en la página **Seleccionar paquete DAC** . Seleccione otro paquete DAC válido o cancele el asistente y genere un nuevo paquete DAC.  
  
 **Validando el contenido de DAC:** barra de progreso que notifica el estado actual del proceso de validación.  
  
 **< Anterior:** vuelve al estado inicial de la página **Seleccionar paquete**.  
  
 **Siguiente>:** avanza a la versión final de la página **Seleccionar paquete**.  
  
 **Cancelar:** termina el asistente sin implementar la DAC.  
  
##  <a name="Review_policy"></a> Página Revisar directiva  
 Use esta página para revisar los resultados de la evaluación de la directiva de selección de servidores de DAC, en caso de que la DAC tenga una directiva. La directiva de selección de servidores de DAC es opcional y está asignada a una DAC que se creó en Microsoft Visual Studio. La directiva se sirve de las facetas de la directiva de selección de servidores para especificar las condiciones que debe cumplir una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] para hospedar la DAC.  
  
 **Resultados de evaluación de condiciones de directivas:** un informe de solo lectura que muestra si se ha cumplido correctamente la evaluación de las condiciones de la directiva de implementación de DAC. Los resultados de la evaluación de cada condición se notifican en una línea independiente.  
  
 **Pasar por alto infracciones de directivas:** use esta casilla para comenzar con la actualización si se produce un error en una o más de las condiciones de la directiva. Seleccione esta opción solamente si está seguro de que todas las condiciones que produjeron errores no evitarán la correcta operación de la DAC.  
  
 **< Anterior:** vuelve a la página **Seleccionar paquete**.  
  
 **Siguiente >:** avanza a la página **Detectar cambio**.  
  
 **Cancelar:** termina el asistente sin actualizar la DAC.  
  
##  <a name="Detect_change"></a> Página Detectar cambio  
 Use esta página para notificar los resultados de la comprobación de los asistentes con respecto a los cambios realizados en la base de datos que hacen que su esquema sea distinto de la definición de esquema almacenada en los metadatos de la DAC en **msdb**. Por ejemplo, si se han usado las instrucciones CREATE, ALTER o DROP para agregar, cambiar o quitar objetos en la base de datos tras la implementación inicial de la DAC. En primer lugar, la página muestra una barra de progreso y, a continuación, notifica los resultados del análisis.  
  
 **Detectando cambio. Esta operación puede tardar algunos minutos:** muestra una barra de progreso mientras el asistente comprueba las diferencias entre el esquema actual de la base de datos y los objetos en la definición de la DAC.  
  
 **Resultado de la detección de cambios:** indica que el análisis se ha completado y los resultados se notifican más abajo.  
  
 **La base de datos DatabaseName no ha cambiado:** el asistente no detectó diferencia alguna en los objetos definidos en la base de datos ni en sus homólogos en la definición de la DAC.  
  
 **La base de datos DatabaseName ha cambiado:** el asistente detectó cambios entre los objetos en la base de datos y sus homólogos en la definición de la DAC.  
  
 **Continuar a pesar de la posible pérdida de los cambios:** indica que entiende que algunos de los objetos o datos en la base de datos actual no estarán presentes en la base de datos nueva y que quiere continuar con la actualización. Seleccione este botón solamente si ha analizado el informe de cambios y entiende los pasos que debe seguir para transferir manualmente cualquier objeto o datos que sean necesarios en la nueva base de datos. Si no está seguro, haga clic en el botón **Guardar informe** para guardar el informe de cambios y, a continuación, haga clic en **Cancelar**. Analice el informe, programe cómo transferir los objetos y datos necesarios una vez se haya completado la actualización y, a continuación, reinicie el asistente.  
  
 **Guardar informe:** haga clic en el botón para guardar un informe de los cambios que el asistente detectó entre los objetos de la base de datos y sus homólogos en la definición de la DAC. A continuación, puede revisar el informe para determinar si necesita tomar medidas cuando se complete la actualización para incorporar algunos o todos los objetos enumerados en el informe dentro de la nueva base de datos.  
  
 **< Anterior:** vuelve a la página **Seleccionar paquete DAC**.  
  
 **Siguiente >**: avanza a la página **Opciones**.  
  
 **Cancelar:** termina el asistente sin implementar la DAC.  
  
## <a name="options-page"></a>Página Opciones  
 Use esta página para seleccionar la reversión en la opción de error para la actualización.  
  
 **Reversión en caso de error** : seleccione esta opción para agregar la actualización en una transacción que el asistente puede intentar revertir si se producen errores. Para obtener más información acerca de la opción, vea [Elegir opciones de actualización de DAC](#ChoseDACUpgOptions).  
  
 **Restaurar valores predeterminados:** devuelve la opción a su valor predeterminado de false.  
  
 **< Anterior:** vuelve a la página **Detectar cambio**.  
  
 **Siguiente >:** avanza a la página **Revisar el plan de actualización**.  
  
 **Cancelar:** termina el asistente sin implementar la DAC.  
  
##  <a name="ReviewUpgPlan"></a> Página Revisar el plan de actualización  
 Use esta página para comprobar las acciones que realizará el proceso de actualización. Continúe solo si está seguro de que la actualización no causará problemas.  
  
 **Se usarán las acciones siguientes para actualizar la DAC.** - Compruebe la información que se muestra para asegurarse de que las acciones emprenda serán las correctas. La columna **Acción** muestra las acciones, como instrucciones Transact-SQL, que se ejecutarán para realizar la actualización. La columna **Pérdida de datos** contendrá una advertencia si la acción asociada puede eliminar datos.  
  
 **Actualizar** : actualiza la lista de acciones.  
  
 **Guardar informe de acciones** : guarda el contenido de la ventana de acción en un archivo HTML.  
  
 **Continuar a pesar de la posible pérdida de los cambios:** indica que entiende que algunos de los objetos o datos en la base de datos actual no estarán presentes en la base de datos nueva y que quiere continuar con la actualización. Seleccione este botón solamente si ha analizado el informe de cambios y entiende los pasos que debe seguir para transferir manualmente cualquier objeto o datos que sean necesarios en la nueva base de datos. Si no está seguro, haga clic en el botón **Guardar informe de acciones** para guardar el informe de cambios y en el botón **Guardar scripts** para guardar el script Transact-SQL; luego, haga clic en **Cancelar**. Analice el informe y el script, planee cómo transferir los objetos y datos necesarios una vez que se haya completado la actualización y, a continuación, reinicie el asistente.  
  
 **Guardar scripts:** guarda en un archivo de texto las instrucciones Transact-SQL que se usarán para realizar la actualización.  
  
 **Restaurar valores predeterminados:** devuelve la opción a su valor predeterminado de false.  
  
 **< Anterior:** vuelve a la página **Detectar cambio**.  
  
 **Siguiente >**: avanza a la página **Resumen**.  
  
 **Cancelar:** termina el asistente sin implementar la DAC.  
  
##  <a name="Summary"></a> Página Resumen  
 Use esta página para realizar una revisión final de las acciones que el asistente realizará al actualizar la DAC.  
  
 **Se usará la siguiente configuración en la actualización de su DAC.** - Compruebe la información que se muestra para asegurarse de que las acciones emprenda serán las correctas. La ventana muestra la DAC que seleccionó para su actualización y el paquete DAC que contiene la nueva versión de la DAC. La ventana también muestra si la versión actual de la base de datos es igual que la definición de la DAC actual, o bien si la base de datos ha cambiado.  
  
 **< Anterior:** vuelve a la página **Revisar el plan de actualización**.  
  
 **Siguiente >**: implementa la DAC y muestra los resultados en la página **Actualizar DAC**.  
  
 **Cancelar:** termina el asistente sin implementar la DAC.  
  
##  <a name="Upgrade"></a> Página Actualizar DAC  
 Esta página notifica si la operación de actualización se realizó correctamente o no.  
  
 **Actualizando la DAC:** indica si cada acción realizada para actualizar la DAC se realizó o no correctamente. Revise la información para determinar si cada acción se realizó o no correctamente. Cualquier acción que encontrara un error tendrá un vínculo en la columna **Resultado** . Seleccione el vínculo para ver un informe del error para esa acción.  
  
 **Guardar informe:** seleccione este botón para guardar el informe de actualización en un archivo HTML. El archivo notifica el estado de cada acción, incluidos todos los errores generados por cualquiera de las acciones. La carpeta predeterminada es una carpeta SQL Server Management Studio\DAC Packages de la carpeta Documentos de su cuenta de Windows.  
  
 **Finalizar** : termina el asistente.  
  
##  <a name="UpgradeDACPowerShell"></a> Usar PowerShell  
 **Para actualizar la DAC con el método IncrementalUpgrade() en un script de PowerShell**  
  
1.  Cree un objeto SMO Server y establézcalo en la instancia que contiene la DAC que se va a actualizar.  
  
2.  Abra un objeto **ServerConnection** y conéctese a la misma instancia.  
  
3.  Use **System.IO.File** para cargar el archivo de paquete DAC.  
  
4.  Use **add_DacActionStarted** y **add_DacActionFinished** para suscribirse a eventos de actualización de la DAC.  
  
5.  Establezca **DacUpgradeOptions**.  
  
6.  Use el método **IncrementalUpgrade** para actualizar la DAC.  
  
7.  Cierra la secuencia de archivos usada para leer el archivo de paquete DAC.  
  
### <a name="example-powershell"></a>Ejemplo (PowerShell)  
 En el ejemplo siguiente se actualiza la DAC denominada MyApplication en una instancia predeterminada de [!INCLUDE[ssDE](../../includes/ssde-md.md)], mediante una nueva versión de la DAC en un paquete MyApplicationVNext.dacpac.  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Open a Common.ServerConnection to the same instance.  
$serverconnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection($srv.ConnectionContext.SqlConnectionObject)  
$serverconnection.Connect()  
$dacstore = New-Object Microsoft.SqlServer.Management.Dac.DacStore($serverconnection)  
  
## Load the DAC package file.  
$dacpacPath = "C:\MyDACs\MyApplicationVNext.dacpac"  
$fileStream = [System.IO.File]::Open($dacpacPath,[System.IO.FileMode]::OpenOrCreate)  
$dacType = [Microsoft.SqlServer.Management.Dac.DacType]::Load($fileStream)  
  
## Subscribe to the DAC upgrade events.  
$dacstore.add_DacActionStarted({Write-Host `n`nStarting at $(get-date) :: $_.Description})  
$dacstore.add_DacActionFinished({Write-Host Completed at $(get-date) :: $_.Description})  
  
## Upgrade the DAC and close the package.  
$dacName  = "MyApplication"  
  
## Set the upgrade options.  
$upgradeProperties = New-Object Microsoft.SqlServer.Management.Dac.DacUpgradeOptions  
$upgradeProperties.blockonchanges = $true  
$upgradeProperties.ignoredataloss = $false  
$upgradeProperties.rollbackonfailure = $true  
$ upgradeProperties.skippolicyvalidation = $false  
  
## Upgrade the DAC  
$dacstore.IncrementalUpgrade($dacName, $dacType, $upgradeProperties)  
## Close the package file.  
$fileStream.Close()  
```  
  
## <a name="see-also"></a>Vea también  
 [Aplicaciones de capa de datos](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  

