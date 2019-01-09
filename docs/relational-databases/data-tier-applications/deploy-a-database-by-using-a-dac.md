---
title: Implementar una base de datos mediante una DAC | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.dbdeployment.settings.f1
- sql13.swb.dbdeployment.progress.f1
- sql13.swb.dbdeployment.summary.f1
- sql13.swb.dbdeployment.results.f1
- sql13.swb.dbdeployment.welcome.f1
helpviewer_keywords:
- deploy database wizard
- database deploy [SQL Server]
ms.assetid: 08c506e8-4ba0-4a19-a066-6e6a5c420539
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d9cdb5c17a74b600b640872d7b153f715da8e15a
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/18/2018
ms.locfileid: "53590239"
---
# <a name="deploy-a-database-by-using-a-dac"></a>Implementar una base de datos mediante una DAC
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Use el asistente para **implementar una base de datos en SQL Azure** para implementar una base de datos entre una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] y un servidor de [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] o entre dos servidores de [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)].  
  
##  <a name="BeforeBegin"></a> Antes de empezar  
 El asistente emplea un archivo de almacenamiento BACPAC de aplicación de capa de datos (DAC) para implementar los datos y las definiciones de los objetos de base de datos. Realiza una operación de exportación de DAC de la base de datos de origen y una importación de DAC al destino.  
  
###  <a name="DBOptSettings"></a> Opciones y configuración de bases de datos  
 De forma predeterminada, la base de datos que se crea durante la implementación tendrá la configuración predeterminada de la instrucción CREATE DATABASE. La excepción es que la intercalación de base de datos y el nivel de compatibilidad se establecen en los valores de la base de datos de origen.  
  
 Algunas opciones de base de datos, como TRUSTWORTHY, DB_CHAINING y HONOR_BROKER_PRIORITY, no se pueden ajustar como parte del proceso de implementación. Las propiedades físicas, como el número de grupos de archivos o el número y tamaño de los archivos no se pueden modificar en el proceso de implementación. Una vez se haya completado la implementación, podrá usar la instrucción ALTER DATABASE, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell para personalizar la base de datos.  
  
###  <a name="LimitationsRestrictions"></a> Limitaciones y restricciones  
 El asistente **Implementar la base de datos** admite implementar una base de datos:  
  
-   Desde una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] en [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)].  
  
-   Desde [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] en una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   Entre dos servidores de [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] .  
  
 El asistente no admite la implementación de bases de datos entre dos instancias del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 Para poder usar el asistente, una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] debe ejecutar [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) o posterior. Si una base de datos de una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] contiene objetos no admitidos en [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)], no puede usar el asistente para implementar la base de datos en [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]. Si una base de datos de [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] contiene objetos no admitidos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], no puede usar el asistente para implementar la base de datos en instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
###  <a name="Security"></a> Seguridad  
 Para mejorar la seguridad, los inicios de sesión de Autenticación de SQL Server están almacenados en un archivo BACPAC de DAC sin contraseña. Cuando se importa el archivo BACPAC, el inicio de sesión se crea como un inicio de sesión deshabilitado con una contraseña generada. Para habilitar los inicios de sesión, use un inicio de sesión que disponga del permiso ALTER ANY LOGIN y emplee ALTER LOGIN para habilitar el inicio de sesión y asignar una nueva contraseña que pueda comunicar al usuario. Esto no se necesita para los inicios de sesión de Autenticación de Windows, porque SQL Server no administra sus contraseñas.  
  
#### <a name="permissions"></a>Permisos  
 El asistente necesita permisos de exportación de DAC en la base de datos de origen. El inicio de sesión necesita al menos permisos ALTER ANY LOGIN y VIEW DEFINITION en el ámbito de la base de datos, así como permisos SELECT en **sys.sql_expression_dependencies**. La exportación de una DAC la pueden realizar los miembros del rol fijo de servidor securityadmin que sean también miembros del rol fijo de base de datos database_owner en la base de datos de la que se exporta la DAC. Los miembros del rol fijo de servidor sysadmin o de la cuenta de administrador del sistema de SQL Server integrada denominada **sa** también pueden exportar una DAC.  
  
 El asistente necesita permisos de importación de DAC en la instancia o el servidor de destino. El inicio de sesión debe ser miembro de los roles fijos de servidor **sysadmin** o **serveradmin** , o del rol fijo de servidor **dbcreator** y disponer de permisos ALTER ANY LOGIN. La cuenta de administrador del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] integrada denominada **sa** también puede importar una DAC. La importación de una DAC con inicios de sesión en [!INCLUDE[ssSDS](../../includes/sssds-md.md)] requiere la pertenencia a los roles loginmanager o serveradmin. La importación de una DAC sin inicios de sesión en [!INCLUDE[ssSDS](../../includes/sssds-md.md)] requiere la pertenencia a los roles dbmanager o serveradmin.  
  
##  <a name="UsingDeployDACWizard"></a> Usar el Asistente para implementar bases de datos  
 **Para migrar una base de datos mediante el Asistente para implementar bases de datos**  
  
1.  Conéctese a la ubicación de la base de datos que desee implementar. Puede especificar una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] o un servidor de [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)] .  
  
2.  En el **Explorador de objetos**, expanda el nodo de la instancia que contiene la base de datos.  
  
3.  Expanda el nodo **Bases de datos** .  
  
4.  Haga clic con el botón derecho en la base de datos que quiera implementar, seleccione **Tareas** y, después, seleccione **Implementar base de datos en SQL Azure...**.  
  
5.  Complete los cuadros de diálogo del asistente:  
  
    -   [Página Introducción](#Introduction)  
  
    -   [Configuración de implementación](#Deployment_settings)  
  
    -   [Página Resumen](#Summary)  
  
    -   [Progreso](#Progress)  
    
    -   [Resultado](#Results)  
  
##  <a name="Introduction"></a> Página Introducción  
 Esta página describe los pasos del asistente **Implementar la base de datos** .  
  
 **Opciones**  
  
-   **No volver a mostrar esta página.** - Active la casilla para que la página Introducción deje de mostrarse en el futuro.  
  
-   **Siguiente** : continúa a la página **Configuración de implementación** .  
  
-   **Cancelar**: cancela la operación y cierra el asistente.  
  
##  <a name="Deployment_settings"></a> Página Configuración de implementación  
 Use esta página para especificar el servidor de destino y proporcionar detalles sobre la nueva base de datos.  
  
 **Host local:**  
  
-   **Conexión de servidor**: especifique los detalles de conexión del servidor y haga clic en **Conectar** para comprobar la conexión.  
  
-   **Nombre de la nueva base de datos**: especifique un nombre para la nueva base de datos.  
  
 **[!INCLUDE[ssSDS](../../includes/sssds-md.md)] :**  
  
-   **Edición de [!INCLUDE[ssSDS](../../includes/sssds-md.md)]**: seleccione la edición de [!INCLUDE[ssSDS](../../includes/sssds-md.md)] en el menú desplegable.  
  
-   **Tamaño máximo de la base de datos**: seleccione el tamaño máximo de la base de datos en el menú desplegable.  
  
 **Otros valores:**  
  
-   Especifique un directorio local para el archivo temporal, que es el archivo de almacenamiento BACPAC. Tenga en cuenta que el archivo se creará en la ubicación especificada y permanecerá en ella una vez completada la operación.  
  
##  <a name="Summary"></a> Página Resumen  
 Esta página se utiliza para revisar los valores de origen y de destino especificados de la operación. Para completar la operación de implementación con los valores especificados, haga clic en **Finalizar**. Para cancelar la operación de implementación y salir del asistente, haga clic en **Cancelar**.  
  
##  <a name="Progress"></a> Página Progreso  
 En esta página se muestra una barra de progreso que indica el estado de la operación. Para ver el estado detallado, haga clic en la opción **Ver detalles** .  
  
##  <a name="Results"></a> Página Resultados  
 En esta página se notifica la corrección o el error de la operación de implementación, mostrando los resultados de cada acción. Cualquier acción que encontrara un error tendrá un vínculo en la columna **Resultado** . Haga clic en el vínculo para ver un informe del error para esa acción.  
  
 Haga clic en **Finalizar** para cerrar el asistente.  
  
## <a name="using-a-net-framework-application"></a>Mediante una aplicación de .Net Framework  
 **Para implementar una base de datos por medio de los métodos Export() e Import() de DacStore en una aplicación de .NET Framework.**  
  
 Para obtener un ejemplo de código, descargue la aplicación de ejemplo de DAC en [Codeplex](https://go.microsoft.com/fwlink/?LinkId=219575).  
  
1.  Cree un objeto SMO Server y establézcalo en la instancia o el servidor que contenga la base de datos que se va a implementar.  
  
2.  Abra un objeto **ServerConnection** y conéctese a la misma instancia.  
  
3.  Use el método **Export** del tipo **Microsoft.SqlServer.Management.Dac.DacStore** para exportar la base de datos a un archivo BACPAC. Especifique el nombre de la base de datos que se exportará y la ruta de acceso a la carpeta donde se va a guardar el archivo BACPAC.  
  
4.  Cree un objeto SMO Server y establézcalo en la instancia o el servidor de destino.  
  
5.  Abra un objeto **ServerConnection** y conéctese a la misma instancia.  
  
6.  Use el método de **Import** del tipo **Microsoft.SqlServer.Management.Dac.DacStore** para importar el archivo BACPAC. Especifique el archivo BACPAC creado por la exportación.  
  
## <a name="see-also"></a>Consulte también  
 [Aplicaciones de capa de datos](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [Exportar una aplicación de capa de datos](../../relational-databases/data-tier-applications/export-a-data-tier-application.md)   
 [Importar un archivo de bacpac para crear una nueva base de datos de usuario](../../relational-databases/data-tier-applications/import-a-bacpac-file-to-create-a-new-user-database.md)  
  
  
