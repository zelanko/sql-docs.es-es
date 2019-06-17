---
title: Registro de una base de datos como una DAC | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.registerdacwizard.registerdac.f1
- sql12.swb.registerdacwizard.summary.f1
- sql12.swb.registerdacwizard.introduction.f1
- sql12.swb.registerdacwizard.setproperties.f1
helpviewer_keywords:
- wizard [DAC], register
- How to [DAC], register
- register DAC
- data-tier application [SQL Server], register
ms.assetid: 08e52aa6-12f3-41dd-a793-14b99a083fd5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1b33e0d78dfe308c537ea5297b55415bce304474
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62918149"
---
# <a name="register-a-database-as-a-dac"></a>Registrar una base de datos como una DAC
  Usar el **registrar el Asistente para aplicaciones de capa de datos** o un Windows script de PowerShell para compilar una definición de aplicación (DAC) de capa de datos que se describe los objetos de base de datos existente y registre la definición de DAC en la `msdb` base de datos del sistema (**maestro** en [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]).  
  
-   **Antes de empezar:**  [Limitaciones y restricciones](#LimitationsRestrictions), [Permisos](#Permissions)  
  
-   **Para actualizar una DAC mediante:**  [el Asistente para registrar aplicación de capa de datos](#UsingRegisterDACWizard), [PowerShell](#RegisterDACPowerShell)  
  
## <a name="before-you-begin"></a>Antes de empezar  
 El proceso de registro crea una definición de DAC que define los objetos de la base de datos. La combinación de la definición de DAC y la base de datos forma una instancia de DAC. Si registra una base de datos como una DA CONTINUACIÓN en una instancia administrada del motor de base de datos, la DAC registrada se incorporará a la Utilidad de SQL Server la próxima vez que el conjunto de recopilación de utilidades se envíe desde la instancia al punto de control de la utilidad. Posteriormente, la DAC aparecerá en el nodo **Aplicaciones de capa de datos implementadas** del [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **Utility Explorer** and reported in the **Aplicaciones de capa de datos implementadas** details page.  
  
###  <a name="LimitationsRestrictions"></a> Limitaciones y restricciones  
 El registro de la DAC solo se puede realizar en una base de datos en [!INCLUDE[ssSDS](../../includes/sssds-md.md)]o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) o posterior. El registro de la DAC no se puede llevar a cabo si una DAC ya está registrada en la base de datos. Por ejemplo, si la base de datos se creó implementando una DAC, no puede ejecutar el **Asistente para registrar aplicación de capa de datos**.  
  
 No puede registra ninguna DAC si la base de datos tiene objetos que no se admiten en una DAC o usuarios contenidos. Para obtener más información acerca de los objetos admitidos por una DAC, vea [DAC Support For SQL Server Objects and Versions](dac-support-for-sql-server-objects-and-versions.md).  
  
###  <a name="Permissions"></a> Permisos  
 El registro de una DAC en una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] requiere, por lo menos, permisos ALTER ANY LOGIN y DEFINITION VIEW en el ámbito de la base de datos, permisos SELECT en **sys.sql_expression_dependencies**y pertenencia al rol fijo de servidor **dbcreator** . Los miembros del rol fijo de servidor **sysadmin** o la cuenta de administrador del sistema de SQL Server integrada denominada **sa** también pueden registrar una DAC. El registro de una DAC que no tiene inicios de sesión en [!INCLUDE[ssSDS](../../includes/sssds-md.md)] requiere la pertenencia a los roles **dbmanager** o **serveradmin** . El registro de una DAC que tiene inicios de sesión en [!INCLUDE[ssSDS](../../includes/sssds-md.md)] requiere la pertenencia a los roles **loginmanager** o **serveradmin** .  
  
##  <a name="UsingRegisterDACWizard"></a> Usar el Asistente para registrar aplicación de capa de datos  
 **Para registrar una DAC mediante un asistente**  
  
1.  En **Explorador de objetos**, expanda el nodo de la instancia que contiene la base de datos que se va a registrar como una DAC.  
  
2.  Expanda el nodo **Bases de datos** .  
  
3.  Haga clic con el botón derecho en la base de datos que se va a registrar, seleccione **Tareas** y después **Registrar como aplicación de capa de datos...**  
  
4.  Complete los cuadros de diálogo del asistente:  
  
    1.  [Página Introducción](#Introduction)  
  
    2.  [Página Definir propiedades](#Set_properties)  
  
    3.  [Página Validación y resumen](#Summary)  
  
    4.  [Página Registrar DAC](#Register)  
  
##  <a name="Introduction"></a> Página Introducción  
 Esta página describe los pasos para registrar una aplicación de capa de datos.  
  
 **No volver a mostrar esta página.** - Haga clic en la casilla para evitar que la página se muestre en el futuro.  
  
 **Siguiente >** : avanza a la página **Definir propiedades**.  
  
 **Cancelar** : sale del asistente sin registrar una DAC.  
  
##  <a name="Set_properties"></a> Página Definir propiedades  
 Use esta página para especificar propiedades en el nivel de DAC como el nombre y la versión de la aplicación.  
  
 **Nombre de aplicación.** - Una cadena que especifica el nombre que se usa para identificar la definición de la DAC; el campo se rellena con el nombre de la base de datos.  
  
 **Versión.** - Un valor numérico que identifica la versión de la DAC. La versión de DAC se usa en Visual Studio para identificar la versión de la DAC en la que están trabajando los desarrolladores. Al implementar una DAC, la versión se almacena en el `msdb` de base de datos y más adelante se pueden ver en el **aplicaciones de capa de datos** nodo [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Descripción.** - Opcional. Texto que explica el propósito de la DAC. Al implementar una DAC, la descripción se almacena en el `msdb` de base de datos y más adelante se pueden ver en el **aplicaciones de capa de datos** nodo [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
 **\< Anterior** -vuelve a la **Introducción** página.  
  
 **Siguiente >** : comprueba que se puede crear una DAC a partir de los objetos de la base de datos y muestra los resultados en la página **Validación y resumen**.  
  
 **Cancelar** : sale del asistente sin registrar la DAC.  
  
##  <a name="Summary"></a> Página Validación y resumen  
 Use esta página para revisar las acciones que el asistente realizará al registrar la DAC. La página pasa por tres estados cuando comprueba que una DAC se puede compilar a partir de los objetos en la base de datos.  
  
### <a name="retrieving-objects"></a>Recuperar objetos  
 **Recuperando la base de datos y los objetos de servidor.** - Muestra una barra de progreso a medida que el asistente recupera todos los objetos necesarios de la base de datos y la instancia del motor de base de datos.  
  
 **\< Anterior** -vuelve a la **Set Properties** página para cambiar las entradas.  
  
 **Siguiente >** : registra la DAC y muestra los resultados en la página **Registrar DAC**.  
  
 **Cancelar** : sale del asistente sin registrar la DAC.  
  
### <a name="validating-objects"></a>Validar objetos  
 **Checking**  _SchemaName_ **.** _ObjectName_ **.** - Muestra una barra de progreso cuando el asistente comprueba las dependencias de los objetos recuperados y comprueba que son todos objetos válidos para una DAC. _SchemaName_ **.** _ObjectName_ identifican el objeto que se está comprobando.  
  
 **\< Anterior** -vuelve a la **Set Properties** página para cambiar las entradas.  
  
 **Siguiente >** : registra la DAC y muestra los resultados en la página **Registrar DAC**.  
  
 **Cancelar** : sale del asistente sin registrar la DAC.  
  
### <a name="summary"></a>Resumen  
 **El siguiente valor se usará para registrar la DAC.** - Muestra un informe de las propiedades y objetos que se incluirán en la DAC.  
  
 **Guardar informe** : seleccione este botón para guardar una copia del informe de validación en un archivo HTML. La carpeta predeterminada es una carpeta **SQL Server Management Studio\DAC Packages** de la carpeta Documentos de su cuenta de Windows.  
  
 **\< Anterior** -vuelve a la **Set Properties** página para cambiar las entradas.  
  
 **Siguiente >** : registra la DAC y muestra los resultados en la página **Registrar DAC**.  
  
 **Cancelar** : sale del asistente sin registrar la DAC.  
  
##  <a name="Register"></a> Página Registrar DAC  
 Esta página notifica si la operación de registro se realizó correctamente o no.  
  
 **Registrando la DAC** : notifica si cada acción realizada para registrar la DAC se realizó correctamente o no. Revise la información para determinar si cada acción se realizó o no correctamente. Cualquier acción que encontrara un error tendrá un vínculo en la columna **Resultado** . Seleccione el vínculo para ver un informe del error para esa acción.  
  
 **Guardar informe** : seleccione este botón para guardar el informe de registro en un archivo HTML. El archivo notifica el estado de cada acción, incluidos todos los errores generados por cualquiera de las acciones. La carpeta predeterminada es una carpeta **SQL Server Management Studio\DAC Packages** de la carpeta Documentos de su cuenta de Windows. El nombre de archivo tiene el formato \<nombreDelPaqueteDAC>_RegisterDACReport_aaaammdd.html, donde \<*nombreDelPaqueteDAC*> es el nombre del paquete que se implementa; *aaaa*, el año actual; *mm*, el mes actual y *dd*, el día actual.  
  
 **Finalizar** : termina el asistente.  
  
##  <a name="RegisterDACPowerShell"></a> Registrar una DAC con PowerShell  
 **Para registrar una base de datos como una DAC mediante el método Register() en un script de PowerShell**  
  
1.  Cree un objeto SMO Server y establézcalo en la instancia que contiene la base de datos que se va a registrar una DAC.  
  
2.  Agregue una variable que especifique el nombre de la base de datos.  
  
3.  Especifique los metadatos de la DAC, como su nombre, versión y descripción.  
  
4.  Ejecute el método Register con la información especificada anteriormente.  
  
### <a name="example-powershell"></a>Ejemplo (PowerShell)  
 El ejemplo siguiente registra una base de datos denominada MyDB como DAC.  
  
```  
## Set a SMO Server object to the default instance on the local computer.  
CD SQLSERVER:\SQL\localhost\DEFAULT  
$srv = get-item .  
  
## Specify the database to register as a DAC.  
$dbname = "MyDB"  
  
## Specify the DAC metadata.  
$applicationname = "MyApplication"  
$version = "1.0.0.0"  
$description = "This DAC defines the database used by my application."  
  
## Register the DAC.  
$registerunit = New-Object Microsoft.SqlServer.Management.Dac.DacExtractionUnit($srv, $dbname, $applicationname, $version)  
$registerunit.Description = $description  
$registerunit.Register()  
```  
  
## <a name="see-also"></a>Vea también  
 [Aplicaciones de capa de datos](data-tier-applications.md)  
  
  
