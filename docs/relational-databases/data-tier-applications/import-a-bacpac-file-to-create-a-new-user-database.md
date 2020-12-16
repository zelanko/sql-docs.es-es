---
description: Importar un archivo de bacpac para crear una nueva base de datos de usuario
title: Importación de un archivo de bacpac para crear una base de datos de usuario
ms.date: 06/03/2020
ms.prod: sql
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb. importdac.results.f1
- sql13.swb.importdac.settings.f1
- sql13.swb.importdac.storagebrowser.f1
- sql13.swb.importdac.results.f1
- sql13.swb.importdac.progress.f1
- sql13.swb. importdac.summary.f1
- sql13.swb.importdac.summary.f1
- sql13.swb. importdac.progress.f1
- sql13.swb.importdac.welcome.f1
- sql13.swb. importdac.settings.f1
helpviewer_keywords:
- Data-tier application
- SQL Server DAC
- Migrate database
- DAC
ms.assetid: 736d8d9a-39f1-4bf8-b81f-2e56c134d12e
author: stevestein
ms.author: sstein
ms.custom: seo-dt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ba8fee19e7b0530bc73157125a025d5a724cbc00
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97481446"
---
# <a name="import-a-bacpac-file-to-create-a-new-user-database"></a>Importar un archivo de bacpac para crear una nueva base de datos de usuario
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Importe un archivo de aplicación de capa de datos (DAC), o archivo .bacpac, para crear una copia de la base de datos original, con los datos, en una instancia nueva de [!INCLUDE[ssDE](../../includes/ssde-md.md)] o en [!INCLUDE[ssSDSFull](../../includes/sssdsfull-md.md)]. Las operaciones de exportación e importación se pueden combinar para migrar una DAC o una base de datos de una instancia a otra, o bien para crear una copia de seguridad lógica, como crear una copia local de una base de datos implementada en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
## <a name="before-you-begin"></a>Antes de empezar  
 El proceso de importación compila una nueva DAC en dos fases.  
  
1.  La importación crea una nueva DAC y la base de datos asociada mediante la definición de DAC almacenada en el archivo de exportación de la misma manera que una implementación de DAC crea una nueva DAC a partir de la definición de un archivo de paquete DAC.  
  
2.  La importación masiva copia los datos del archivo de exportación.  

## <a name="sql-server-utility"></a>Utilidad de SQL Server  
 Si importa una DAC en una instancia del motor de base de datos, la DAC importada se incorpora a la Utilidad de SQL Server la próxima vez que el conjunto de recopilación de utilidades se envíe desde la instancia al punto de control de la utilidad. Posteriormente, la DAC aparecerá en el nodo **Aplicaciones de capa de datos implementadas** del [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] **Explorador de la utilidad** y se notificará en la página de detalles **Aplicaciones de capa de datos implementadas**.  
  
## <a name="database-options-and-settings"></a>Opciones y configuración de bases de datos  
 De forma predeterminada, la base de datos creada durante la importación incorporará toda la configuración predeterminada de la instrucción CREATE DATABASE, con la excepción de que la intercalación de base de datos y el nivel de compatibilidad se establecen en los valores definidos en el archivo de exportación de DAC. Un archivo de exportación de DAC usa los valores de la base de datos original.  
  
 Algunas opciones de base de datos, como TRUSTWORTHY, DB_CHAINING y HONOR_BROKER_PRIORITY, no se pueden ajustar en el proceso de importación. Las propiedades físicas, como el número de grupos de archivos o el número y tamaño de los archivos no se pueden modificar en el proceso de importación. Una vez se haya completado la importación, podrá usar la instrucción ALTER DATABASE, [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell para personalizar la base de datos. Para obtener más información, consulte [Databases](../../relational-databases/databases/databases.md).  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 Se puede importar una DAC en [!INCLUDE[ssSDS](../../includes/sssds-md.md)]o en una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] que ejecute [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Service Pack 4 (SP4) o posterior. Si exporta una DAC de una versión anterior, puede contener objetos que [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]no admita. No puede implementar dicha DAC en instancias de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
## <a name="prerequisites"></a>Requisitos previos  
 Se recomienda no importar un archivo de exportación de DAC desde orígenes desconocidos o que no sean de confianza. Es posible que estos archivos contengan código malintencionado que podría ejecutar código Transact-SQL no deseado o provocar errores al modificar el esquema o la estructura de la base de datos física. Antes de usar un archivo de exportación de un origen desconocido o que no sea de confianza, desempaquete la DAC y examine el código, como procedimientos almacenados y otro código definido por el usuario. Para obtener más información acerca de cómo realizar estas comprobaciones, vea [Validate a DAC Package](validate-a-dac-package.md).  
  
## <a name="security"></a>Seguridad  
 Para mejorar la seguridad, los inicios de sesión de autenticación de SQL Server están almacenados en un archivo de exportación de DAC sin contraseña. Cuando el archivo se importa, el inicio de sesión se crea como un inicio de sesión deshabilitado con una contraseña generada. Para habilitar los inicios de sesión, use un inicio de sesión que disponga del permiso ALTER ANY LOGIN y utilice ALTER LOGIN para habilitar el inicio de sesión y asignar una contraseña nueva que se pueda comunicar al usuario. Esto no se necesita para los inicios de sesión de Autenticación de Windows, porque SQL Server no administra sus contraseñas.  
  
## <a name="permissions"></a>Permisos  
 Una DAC solo la pueden importar miembros de los roles fijos de servidor **sysadmin** o **serveradmin** , o inicios de sesión que pertenezcan al rol fijo de servidor **dbcreator** y dispongan de permisos ALTER ANY LOGIN. La cuenta de administrador del sistema de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] integrada denominada **sa** también puede importar una DAC. La importación de una DAC con inicios de sesión en [!INCLUDE[ssSDS](../../includes/sssds-md.md)] requiere la pertenencia a los roles loginmanager o serveradmin. La importación de una DAC sin inicios de sesión en [!INCLUDE[ssSDS](../../includes/sssds-md.md)] requiere la pertenencia a los roles dbmanager o serveradmin.  
  
## <a name="using-the-import-data-tier-application-wizard"></a>Usar el Asistente Importar aplicación de capa de datos  
 **Para iniciar el asistente, realice los pasos siguientes:**  
  
1.  Conéctese con la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ya sea local o en [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
2.  En el **Explorador de objetos**, haga clic con el botón derecho en **Bases de datos** y, después, seleccione el elemento de menú **Importar aplicación de capa de datos** para iniciar el asistente.  
  
3.  Complete los cuadros de diálogo del asistente:  
  
    -   [Página Introducción](#Introduction)  
  
    -   [Página Importar configuración](#Import_settings)  
  
    -   [Página Configuración de base de datos](#Database_settings)  
  
    -   [Página Resumen](#Summary)  
  
    -   [Página Progreso](#Progress)  
  
    -   [Página Resultados](#Results)  
  
###  <a name="introduction-page"></a><a name="Introduction"></a> Página Introducción  
 Esta página describe los pasos para el Asistente Importar aplicación de capa de datos.  
  
 **Opciones**  
  
-   **No volver a mostrar esta página.** - Active la casilla para que la página Introducción deje de mostrarse en el futuro.  
  
-   **Siguiente**: continúa a la página **Importar configuración**.  
  
-   **Cancelar**: cancela la operación y cierra el asistente.  
  
###  <a name="import-settings-page"></a><a name="Import_settings"></a> Página Importar configuración  
 Use esta página para especificar la ubicación del archivo .bacpac para importar.  
  
-   **Importar desde el disco local**: haga clic en **Examinar...** para navegar por el equipo local, o bien especifique la ruta de acceso en el espacio proporcionado. El nombre de ruta de acceso debe incluir un nombre de archivo y la extensión .bacpac.  
  
-   **Importar desde Azure**: importa un archivo BACPAC desde un contenedor de Microsoft Azure. Debe conectarse a un contenedor de Microsoft Azure para validar esta opción. Tenga en cuenta que la opción Importar desde Azure también requiere que se especifique un directorio local para el archivo temporal. El archivo temporal se creará en la ubicación especificada y permanecerá allí una vez finalizada la operación.  
  
     Al examinar Azure, podrá intercambiar entre los contenedores de una cuenta única. Debe especificar un único archivo .bacpac para continuar con la operación de importación. Puede ordenar las columnas por **Nombre**, **Tamaño** o **Fecha de modificación**.  
  
     Para continuar, especifique el archivo .bacpac para importar y, a continuación, haga clic en **Abrir**.  
  
###  <a name="database-settings-page"></a><a name="Database_settings"></a> Página Configuración de base de datos  
 Use esta página para especificar los detalles de la base de datos que se creará.  
  
 **Para una instancia local de SQL Server:**  
  
-   **Nombre de la nueva base de datos**: proporcione un nombre para la base de datos importada.  
  
-   **Ruta de acceso del archivo de datos**: proporcione un directorio local para los archivos de datos. Haga clic en **Examinar...** para navegar por el equipo local, o bien especifique la ruta de acceso en el espacio proporcionado.  
  
-   **Ruta de acceso del archivo de registro**: especifique un directorio local para los archivos de registro. Haga clic en **Examinar...** para navegar por el equipo local, o bien especifique la ruta de acceso en el espacio proporcionado.  
  
 Para continuar, haga clic en **Siguiente**.  
  
 **Desde Azure SQL Database:**  
  
 - En **[Importación de un archivo BACPAC para crear una instancia de Azure SQL Database](/azure/azure-sql/database/database-import)** se proporcionan instrucciones paso a paso con Azure Portal, PowerShell, SSMS o SqlPackage.  
 - Consulte **[Opciones y rendimiento de SQL Database: descripción de lo que está disponible en cada nivel de servicio](/azure/azure-sql/database/purchasing-models)** para obtener una vista detallada de los distintos niveles de servicio.  

### <a name="validation-page"></a>Página Validación  
 Use esta página para revisar los problemas que bloquean la operación. Para continuar, resuelva los problemas de bloqueo y, después, haga clic en **Volver a ejecutar la validación** para asegurarse de que la validación es correcta.  
  
 Para continuar, haga clic en **Siguiente**.  
  
###  <a name="summary-page"></a><a name="Summary"></a> Página Resumen  
 Esta página se utiliza para revisar los valores de origen y de destino especificados de la operación. Para completar la operación de importación mediante los valores especificados, haga clic en **Finalizar**. Para cancelar la operación de importación y salir del asistente, haga clic en **Cancelar**.  
  
###  <a name="progress-page"></a><a name="Progress"></a> Página Progreso  
 En esta página se muestra una barra de progreso que indica el estado de la operación. Para ver el estado detallado, haga clic en la opción **Ver detalles** .  
  
 Para continuar, haga clic en **Siguiente**.  
  
###  <a name="results-page"></a><a name="Results"></a> Página Resultados  
 Esta página notifica el éxito o error de importación y crea las operaciones de la base de datos, mostrando el éxito o error de cada acción. Cualquier acción que encontrara un error tendrá un vínculo en la columna **Resultado** . Haga clic en el vínculo para ver un informe del error para esa acción.  
  
 Haga clic en **Cerrar** para cerrar el asistente.  
  
## <a name="see-also"></a>Vea también  
[Importar un archivo BACPAC para crear una base de datos de Azure SQL](/azure/azure-sql/database/database-import)  
 [Aplicaciones de capa de datos](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [Exportar una aplicación de la capa de datos](../../relational-databases/data-tier-applications/export-a-data-tier-application.md)  
  
