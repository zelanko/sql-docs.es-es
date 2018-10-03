---
title: Implementación de una base de datos de SQL Server en una máquina virtual de Microsoft Azure | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.deploymentwizard.deploymentsettings.f1
- sql12.swb.deploymentwizard.progress.f1
- sql11.swb.usevmdialog.f1
- sql11.swb.deploymentwizard.f1
- sql12.swb.deploymentwizard.azuresignin.f1
- sql11.swb.deploymentwizard.summary.f1
- sql11.swb.deploymentwizard.azuresignin.f1
- sql12.swb.deploymentwizard.f1
- sql12.swb.sqlvmdialog.f1
- sql11.swb.newvmdialog.f1
- sql12.swb.deploymentwizard.results.f1
- sql11.swb.deploymentwizard.progress.f1
- sql12.swb.newvmdialog.f1
- sql12.swb.deploymentwizard.sourcesettings.f1
- sql12.swb.usevmdialog.f1
- sql11.swb.deploymentwizard.sourcesettings.f1
- sql11.swb.deploymentwizard.results.f1
- sql12.swb.deploymentwizard.summary.f1
- sql11.swb.deploymentwizard.deploymentsettings.f1
helpviewer_keywords:
- Deploy a database
- Deploy to Azure VM
- Migrate to Azure
- Windows Azure virtual machine
- Migrate to Azure VM
- Migrate to the cloud
- SQL Server Management Studio
- SSMS
- Deploy database wizard
- Deploy a SQL Server database to Azure
- Azure VM
ms.assetid: 5e82e66a-262e-4d4f-aa89-39cb62696d06
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c17e29b5a41930f954e5cad6b67fccbaa1cc086d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48207535"
---
# <a name="deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine"></a>Implementar una base de datos de SQL Server en una máquina virtual de Microsoft Azure
  Use la **implementar una base de datos de SQL Server en una máquina virtual de Windows Azure** Asistente para implementar una base de datos de una instancia de la [!INCLUDE[ssDE](../../includes/ssde-md.md)] a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en una máquina Virtual de Azure de Windows (VM). El asistente emplea una operación de copia de seguridad completa de la base de datos, por lo que siempre copia todo el esquema de la base de datos y los datos de una base de datos de usuario de SQL Server. El asistente también realiza toda la configuración de Azure VM, por lo que no se requiere ninguna configuración previa de la VM.  
  
 No puede usar el asistente para las copias de seguridad diferenciales porque no sobrescribirá una base de datos existente que tenga el mismo nombre de base de datos. Para reemplazar una base de datos existente en la VM, debe quitar primero la base de datos existente o cambiar el nombre de la base de datos. Si hay un conflicto de nombres entre el nombre de la base de datos para una operación de implementación en ejecución y una base de datos existente en la VM, el asistente sugerirá un nombre de base de datos anexado para la base de datos en ejecución de manera que pueda completar la operación.  
  
##  <a name="before_you_begin"></a> Antes de comenzar  
 Para completar este asistente, debe poder proporcionar la siguiente información y tener esta configuración:  
  
-   Los detalles de la cuenta de Microsoft asociados a la suscripción de Windows Azure.  
  
-   El perfil de publicación de Windows Azure.  
  
    > [!CAUTION]  
    >  SQL Server admite actualmente la versión 2.0 del perfil de publicación. Para descargar la versión compatible del perfil de publicación, vea [Descargar perfil de publicación 2.0](http://go.microsoft.com/fwlink/?LinkId=396421).  
  
-   El certificado de administración cargado para la suscripción de Windows Azure.  
  
-   El certificado de administración guardado en el almacén de certificados personal en el equipo en el que se está ejecutando el asistente.  
  
-   Debe tener una ubicación de almacenamiento temporal que esté disponible en el equipo donde se hospede la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La ubicación de almacenamiento temporal también debe estar disponible en el equipo donde el asistente se esté ejecutando.  
  
-   Si está implementando la base de datos en una VM existente, la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe estar configurada para escuchar en un puerto TCP/IP.  
  
-   La VM de Windows Azure o la imagen de la Galería que pretende usar para la creación de la VM debe tener el adaptador para la nube de SQL Server configurado y en ejecución.  
  
-   Debe configurar un extremo abierto para el adaptador para la nube de SQL Server en la puerta de enlace de Windows Azure con el puerto privado 11435.  
  
 Además, si piensa implementar la base de datos en una VM de Windows Azure existente, también debe poder proporcionar:  
  
-   El nombre DNS del servicio en la nube que hospeda la VM.  
  
-   Credenciales de administrador para la VM.  
  
-   Credenciales con privilegios de operador de copia de seguridad en la base de datos que pretende implementar, desde la instancia de origen de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para obtener más información sobre la ejecución de SQL Server en máquinas virtuales de Windows Azure, consulte [preparar la migración a SQL Server en Microsoft Azure Virtual Machines](http://msdn.microsoft.com/library/dn133142.aspx).  
  
 En los equipos que ejecutan sistemas operativos Windows Server, debe usar la configuración siguiente para ejecutar este asistente:  
  
-   Desactive la Configuración de seguridad mejorada: use Administrador del servidor > Servidor local para establecer la Configuración de seguridad mejorada (ESC) de Internet Explorer en **DESACTIVADA**.  
  
-   Habilitar JavaScript: Internet Explorer > Opciones de Internet > Seguridad > Nivel personalizado > Scripting > Active scripting: **Habilitar**.  
  
###  <a name="limitations"></a> Limitaciones y restricciones  
 La limitación de tamaño de la base de datos para esta operación es 1 TB.  
  
 Esta característica de implementación está disponible en SQL Server Management Studio para [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
 Esta característica de implementación solo se puede usar con bases de datos de usuario; no se admite implementar bases de datos del sistema.  
  
 La característica de implementación no admite los servicios hospedados asociados a un grupo de afinidad. Por ejemplo, las cuentas de almacenamiento asociadas a un grupo de afinidad no se pueden seleccionar para usarlas en la página **Configuración de implementación** de este asistente.  
  
 La versión de SQL Server de la máquina virtual debe ser igual o posterior a la versión de SQL Server de origen. Las versiones de la base de datos de SQL Server que se pueden implementar en la máquina virtual de Windows Azure con este asistente son:  
  
-   SQL Server 2008  
  
-   SQL Server 2008 R2  
  
-   SQL Server 2012  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
 Las versiones de la base de datos de SQL Server que se ejecutan en una base de datos de la VM de Windows Azure se pueden implementar en:  
  
-   SQL Server 2012  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
 Si hay un conflicto de nombres entre el nombre de la base de datos para una operación de implementación en ejecución y una base de datos existente en la VM, el asistente sugerirá un nombre de base de datos anexado para la base de datos en ejecución de manera que pueda completar la operación.  
  
###  <a name="filestream"></a> Consideraciones para implementar una base de datos habilitada para FILESTREAM en una máquina virtual de Windows Azure  
 Tenga en cuenta las directrices y limitaciones siguientes al implementar las bases de datos que tienen BLOBS almacenados en objetos FILESTREAM:  
  
-   La característica de implementación no puede implementar una base de datos habilitada para FILESTREAM en una nueva máquina virtual. Si FILESTREAM no está habilitado en la máquina virtual antes de ejecutar el asistente, la operación de restauración de la base de datos producirá un error y la operación del asistente no se podrá completar correctamente. Para implementar correctamente una base de datos que utiliza FILESTREAM, habilite FILESTREAM en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la máquina virtual host antes de iniciar el asistente. Para obtener más información, vea [FILESTREAM (SQL Server)](http://msdn.microsoft.com/library/gg471497.aspx).  
  
-   Si la base de datos utiliza OLTP en memoria, puede implementar la base de datos en una máquina virtual de Windows Azure sin ninguna modificación en la base de datos. Para obtener más información, vea [OLTP en memoria (optimización en memoria)](http://msdn.microsoft.com/library/dn133186\(SQL.120\).aspx).  
  
###  <a name="geography"></a> Consideraciones acerca de la distribución geográfica de activos  
 Observe que los activos siguientes se deben encontrar en la misma región geográfica:  
  
-   Servicio en la nube  
  
-   Ubicación de máquina virtual  
  
-   Servicio de almacenamiento en disco de datos  
  
 Si los activos enumerados anteriormente no se ubican conjuntamente, el asistente no se podrá completar correctamente.  
  
###  <a name="configuration_settings"></a> Valores de configuración del asistente  
 Utilice los detalles siguientes de configuración para modificar la configuración de una implementación de la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en una máquina virtual de Windows Azure.  
  
-   **Ruta de acceso predeterminada del archivo de configuración** : %LOCALAPPDATA%\SQL Server\Deploy to SQL in WA VM\DeploymentSettings.xml  
  
-   **Estructura de los archivos de configuración**  
  
    -   \<DeploymentSettings>  
  
        -   <OtherSettings  
  
            -   TraceLevel="Debug" \<!-- Nivel de registro -->  
  
            -   BackupPath="\\\\[nombre de servidor]\\[volumen]\\" \<!-- La última ruta de acceso usada para la copia de seguridad. Se usa como valor predeterminado del asistente. -->  
  
            -   CleanupDisabled = False /> \<! -- El asistente no eliminará los archivos intermedios y objetos de Windows Azure (VM, CS, SA). -->  
  
        -   <PublishProfile \<! -- La última información usada del perfil de publicación. -->  
  
            -   Certificate="12A34B567890123ABCD4EF567A8" \<!-- El certificado que se debe usar en el asistente. -->  
  
            -   Subscription="1a2b34c5-67d8-90ef-ab12-xxxxxxxxxxxxx" \<!-- La suscripción que se debe usar en el asistente. -->  
  
            -   Name="Mi suscripción" \<! -- El nombre de la suscripción. -->  
  
            -   Publisher="" />  
  
    -   \</DeploymentSettings>  
  
 **Valores del archivo de configuración**  
  
###  <a name="permissions"></a> Permissions  
 La base de datos que se implementa debe estar en un estado normal, la base de datos debe ser accesible para la cuenta de usuario que ejecuta el asistente y la cuenta de usuario debe tener permisos para realizar una operación de copia de seguridad.  
  
##  <a name="launch_wizard"></a> Uso de la base de datos de implementación para el Asistente para la máquina virtual de Azure de Windows  
 **Para iniciar el asistente, realice los pasos siguientes:**  
  
1.  Use SQL Server Management Studio para conectarse a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la base de datos que desea implementar.  
  
2.  En el **Explorador de objetos**, expanda el nombre de instancia y, a continuación, expanda el nodo **Bases de datos** .  
  
3.  Haga clic con el botón secundario en la base de datos que desee implementar, seleccione **Tareas**y, a continuación, seleccione **Implementar base de datos en VM de Windows Azure…**.  
  

  
##  <a name="Introduction"></a> Página Introducción  
 Esta página describe el asistente para **Implementar una base de datos de SQL Server en Windows VM Azure** .  
  
 **Opciones**  
  
-   **No volver a mostrar esta página.** - Active esta casilla para que la página Introducción deje de mostrarse en el futuro.  
  
-   **Siguiente** : continúa en la página **Configuración de origen** .  
  
-   **Cancelar** : cancela la operación y cierra el asistente.  
  
-   **Ayuda** : inicia el tema de Ayuda de MSDN para el asistente.  
  
##  <a name="Source_settings"></a> Configuración de origen  
 Utilice esta página para conectarse a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda la base de datos que desea implementar en la máquina virtual de Windows Azure. También especificará una ubicación temporal para que los archivos se guarden del equipo local antes de que se transfieran a Windows Azure. Esta puede ser una ubicación de red compartida.  
  
 **Opciones**  
  
-   Haga clic en **Conectar** y, a continuación, especifique los detalles de conexión para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda la base de datos para implementar.  
  
-   Use la lista desplegable **Seleccionar base de datos** para especificar la base de datos que implementar.  
  
-   En el campo **Otras configuraciones** , especifique una carpeta compartida que estará accesible para el servicio VM de Windows Azure.  
  
##  <a name="Azure_sign-in"></a> Windows Azure inicio de sesión  
 Utilice esta página para conectarse a Windows Azure y proporcionar los detalles del perfil de publicación o del certificado de administración.  
  
 **Opciones**  
  
-   **Certificado de administración** : utilice esta opción para especificar un certificado del almacén de certificados local que coincida con el certificado de administración de Windows Azure.  
  
-   **Perfil de publicación** : utilice esta opción si ya tiene un perfil de publicación descargado en el equipo.  
  
-   **Iniciar sesión** : use esta opción para firmar en Windows Azure con una cuenta de Microsoft, por ejemplo, una cuenta de Hotmail o Live ID, para generar y descargar un nuevo certificado de administración. Observe que el número de certificados por suscripción está limitado.  
  
-   **Suscripción** : seleccione el tipo o pegue el identificador de su suscripción de Windows Azure que coincida con el certificado de administración del almacén de certificados local o un perfil de publicación.  
  
##  <a name="Deployment_settings"></a> Página Configuración de implementación  
 Use esta página para especificar el servidor de destino y proporcionar detalles sobre la nueva base de datos.  
  
 **Opciones**  
  
-   **Máquina virtual de Azure** : especifica los detalles de la VM que hospedará la base de datos de SQL Server:  
  
-   **Nombre del servicio en la nube** : especifique el nombre del servicio que hospeda la VM. Para crear un nuevo servicio en la nube, especifique un nombre para este.  
  
-   **Nombre de máquina virtual** : especifique el nombre de la VM que hospedará la base de datos de SQL Server. Para crear una nueva VM de Windows Azure, especifique un nombre para esta.  
  
-   **Configuración** : use el botón Configuración para crear una nueva VM para hospedar la base de datos de SQL Server. Si está utilizando una VM existente, la información que proporcione se utilizará para autenticar las credenciales.  
  
-   **Cuenta de almacenamiento** : seleccione la cuenta de almacenamiento en la lista desplegable. Para crear una nueva cuenta de almacenamiento, especifique un nombre para esta. Observe que las cuentas de almacenamiento asociadas a un grupo de afinidad no estarán disponibles en la lista desplegable.  
  
-   **Base de datos de destino** : especifica los detalles de la base de datos de destino.  
  
-   **Conexión al servidor** : detalles de conexión del servidor.  
  
-   **Base de datos** : especifique o confirme el nombre de una nueva base de datos. Si el nombre de la base de datos ya existe en la instancia de SQL Server de destino, se recomienda especificar un nombre de base de datos modificado.  
  
##  <a name="Summary"></a> Página Resumen  
 Esta página se utiliza para revisar la configuración especificada para la operación. Para completar la operación de implementación con los valores especificados, haga clic en **Finalizar**. Para cancelar la operación de implementación y salir del asistente, haga clic en **Cancelar**.  
  
 Puede haber pasos manuales que sean necesarios para implementar los detalles de la base de datos en la base de datos de SQL Server en la VM de Windows Azure. Estos pasos se describen en detalle.  
  
##  <a name="Results"></a> Página Resultados  
 En esta página se notifica la corrección o el error de la operación de implementación, mostrando los resultados de cada acción. Cualquier acción que encuentre un error tendrá una indicación en la columna **Resultado** . Haga clic en el vínculo para ver un informe del error para esa acción.  
  
 Haga clic en **Finalizar** para cerrar el asistente.  
  
## <a name="see-also"></a>Vea también  
 [adaptador para la nube de SQL Server](../../database-engine/cloud-adapter-for-sql-server.md)   
 [Administración del ciclo de vida de base de datos](../database-lifecycle-management.md)   
 [Exportar una aplicación de capa de datos](../data-tier-applications/export-a-data-tier-application.md)   
 [Importar un archivo de bacpac para crear una nueva base de datos de usuario](../data-tier-applications/import-a-bacpac-file-to-create-a-new-user-database.md)   
 [Copias de seguridad y restauración de bases de datos SQL de Azure](https://msdn.microsoft.com/library/azure/jj650016.aspx)   
 [Implementación de SQL Server en máquinas virtuales de Microsoft Azure](http://msdn.microsoft.com/library/dn133141.aspx)   
 [Preparación para la migración a SQL Server en máquinas virtuales de Microsoft Azure](http://msdn.microsoft.com/library/dn133142.aspx)  
  
  
