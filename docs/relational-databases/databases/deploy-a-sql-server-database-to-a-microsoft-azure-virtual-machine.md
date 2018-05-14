---
title: Implementación de una base de datos de SQL Server en una máquina virtual de Microsoft Azure | Microsoft Docs
ms.date: 07/29/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: databases
ms.reviewer: ''
ms.suite: sql
ms.custom: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.swb.deploymentwizard.deploymentsettings.f1
- sql13.swb.deploymentwizard.sourcesettings.f1
- sql13.swb.deploymentwizard.summary.f1
- sql13.swb.agdashboard.agp9virtualnw.issues.f1
- sql13.swb.deploymentwizard.f1
- sql13.swb.deploymentwizard.progress.f1
- sql13.swb.usevmdialog.f1
- sql13.swb.newvmdialog.f1
- sql13.swb.sqlvmdialog.f1
- sql13.swb.deploymentwizard.results.f1
- sql13.swb.deploymentwizard.azuresignin.f1
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
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3ad29084eda4f085e090ec9f436a5dd3f170429f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="deploy-a-sql-server-database-to-a-microsoft-azure-virtual-machine"></a>Implementar una base de datos de SQL Server en una máquina virtual de Microsoft Azure
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use el asistente para **Implementar una base de datos en una máquina virtual de Microsoft Azure** para implementar una base de datos desde una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en una máquina virtual (VM) de Microsoft Azure. El asistente emplea una operación de copia de seguridad completa de la base de datos, por lo que siempre copia todo el esquema de la base de datos y los datos de una base de datos de usuario de SQL Server. El asistente también realiza toda la configuración de Azure VM, por lo que no se requiere ninguna configuración previa de la VM.  
  
 No puede usar el asistente para copias de seguridad diferenciales. El asistente no sobrescribirá una base de datos existente que tiene el mismo nombre de base de datos. Para reemplazar una base de datos existente en la VM, debe quitar primero la base de datos existente o cambiar el nombre de la base de datos. Si hay un conflicto de nombres entre el nombre de la base de datos para una operación de implementación en ejecución y una base de datos existente en la VM, el asistente sugerirá un nombre de base de datos anexado para la base de datos en ejecución de manera que pueda completar la operación.  
  
-   [Antes de comenzar](#before_you_begin)  
  
-   [Limitaciones y restricciones](#limitations)  
  
-   [Consideraciones para implementar una base de datos habilitada para FILESTREAM](#filestream)  
  
-   [Consideraciones acerca de la distribución geográfica de activos](#geography)  
  
-   [Valores de configuración del asistente](#configuration_settings)  
  
-   [Permisos necesarios](#permissions)  
  
-   [Iniciar el asistente](#launch_wizard)  
  
-   [Páginas del asistente](#wizard_pages)  
  
> [!NOTE]  
>  Para un tutorial detallado paso a paso de este asistente, consulte [Migración de una Base de datos SQL Server a SQL Server en una máquina virtual de Azure](https://azure.microsoft.com/en-us/documentation/articles/virtual-machines-migrate-onpremises-database/).  
  
##  <a name="before_you_begin"></a> Antes de comenzar  
 Para completar este asistente, debe poder proporcionar la siguiente información y tener esta configuración:  
  
-   Los detalles de la cuenta de Microsoft asociados a la suscripción de Windows Azure.  
  
-   El perfil de publicación de Windows Azure.  
  
    > [!CAUTION]  
    >  SQL Server admite actualmente la versión 2.0 del perfil de publicación. Para descargar la versión compatible del perfil de publicación, vea [Descargar perfil de publicación 2.0](http://go.microsoft.com/fwlink/?LinkId=396421).  
  
-   El certificado de administración cargado para la suscripción a Microsoft Azure.  Cree el certificado de administración con el cmdlet [New-SelfSignedCertificate](https://technet.microsoft.com/library/hh848633(v=wps.630))de PowerShell.  Luego, cargue el certificado de administración a la suscripción de Microsoft Azure.  Para más información sobre cómo cargar un certificado de administración, consulte [Carga de un certificado de administración de API de Administración de Azure](https://azure.microsoft.com/en-us/documentation/articles/azure-api-management-certs/).  Sintaxis de ejemplo para crear un certificado de administración desde [Introducción a los certificados para Azure Cloud Services](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-certs-create/): 

    ```powershell  
    $cert = New-SelfSignedCertificate -DnsName yourdomain.cloudapp.net -CertStoreLocation "cert:\LocalMachine\My"
    $password = ConvertTo-SecureString -String "your-password" -Force -AsPlainText
    Export-PfxCertificate -Cert $cert -FilePath ".\my-cert-file.pfx" -Password $password
    ```    

    > [!NOTE]  
    > También se puede usar la herramienta MakeCert para crear un certificado de administración; sin embargo, MakeCert ahora está en desuso.  Para información adicional, consulte [MakeCert](https://msdn.microsoft.com/library/windows/desktop/aa386968).
   
  -   El certificado de administración guardado en el almacén de certificados personal en el equipo en el que se está ejecutando el asistente.  
  
-   Debe tener una ubicación de almacenamiento temporal que esté disponible en el equipo donde se hospede la base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La ubicación de almacenamiento temporal también debe estar disponible en el equipo donde el asistente se esté ejecutando.  
  
-   Si está implementando la base de datos en una VM existente, la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe estar configurada para escuchar en un puerto TCP/IP.  
  
-   La VM de Microsoft Azure o la imagen de la Galería que pretende usar para la creación de la máquina virtual debe tener el [adaptador para la nube de SQL Server](http://msdn.microsoft.com/library/82ed0d0f-952d-4d49-aa36-3855a3ca9877) configurado y en ejecución.  
  
-   Debe configurar un punto de conexión abierto para el [adaptador para la nube de SQL Server](http://msdn.microsoft.com/library/82ed0d0f-952d-4d49-aa36-3855a3ca9877) en la puerta de enlace de Microsoft Azure con el puerto privado 11435.  
  
 Además, si piensa implementar la base de datos en una VM de Windows Azure existente, también debe poder proporcionar:  
  
-   El nombre DNS del servicio en la nube que hospeda la VM.  
  
-   Credenciales de administrador para la VM.  
  
-   Credenciales con privilegios de operador de copia de seguridad en la base de datos que pretende implementar, desde la instancia de origen de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Para más información sobre cómo ejecutar SQL Server en máquinas virtuales de Microsoft Azure, consulte [Aprovisionamiento de una máquina virtual de SQL Server en el Portal de Azure](https://msdn.microsoft.com/library/dn133141.aspx) y [Migración de una Base de datos SQL Server a SQL Server en una máquina virtual de Azure](http://msdn.microsoft.com/library/dn133142.aspx).  
  
 En los equipos que ejecutan sistemas operativos Windows Server, debe usar la configuración siguiente para ejecutar este asistente:  
  
-   Desactive la Configuración de seguridad mejorada: use Administrador del servidor > Servidor local para establecer la Configuración de seguridad mejorada (ESC) de Internet Explorer en **DESACTIVADA**.  
  
-   Habilitar JavaScript: Internet Explorer > Opciones de Internet > Seguridad > Nivel personalizado > Scripting > Active scripting: **Habilitar**.  
  
###  <a name="limitations"></a> Limitaciones y restricciones  
Esta característica de implementación solo se usa con una cuenta de almacenamiento de Azure que se haya creado con el modelo de implementación de Service Management (clásico). Para obtener más información sobre los modelos de implementación de Azure, vea [La implementación de Azure Resource Manager frente a la implementación clásica: los modelos de implementación y el estado de los recursos](https://azure.microsoft.com/en-us/documentation/articles/resource-manager-deployment-model/).

 La limitación de tamaño de la base de datos para esta operación es 1 TB.  
  
 Esta característica de implementación está disponible en SQL Server Management Studio para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
 Esta característica de implementación solo se puede usar con bases de datos de usuario; no se admite implementar bases de datos del sistema.  
  
 La característica de implementación no admite los servicios hospedados asociados a un grupo de afinidad. Por ejemplo, las cuentas de almacenamiento asociadas a un grupo de afinidad no se pueden seleccionar para usarlas en la página **Configuración de implementación** de este asistente.  
  
 Las versiones de la base de datos de SQL Server que se pueden implementar en la máquina virtual de Windows Azure con este asistente son:  
  
-   SQL Server 2008  
  
-   SQL Server 2008 R2  
  
-   SQL Server 2012  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  

- [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 Las versiones de la base de datos de SQL Server que se ejecutan en una base de datos de la VM de Windows Azure se pueden implementar en:  
  
-   SQL Server 2012  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  

- [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
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
  
        -   \<OtherSettings  
  
            -   TraceLevel="Debug" \<!-- Nivel de registro -->  
  
            -   BackupPath="\\\\[nombre de servidor]\\[volumen]\\" \<!-- La última ruta de acceso usada para la copia de seguridad. Se usa como valor predeterminado del asistente. -->  
  
            -   CleanupDisabled = False /> \<! -- El asistente no eliminará los archivos intermedios y objetos de Windows Azure (VM, CS, SA). -->  
  
        -   \<PublishProfile \<!-- La última información usada del perfil de publicación. -->  
  
            -   Certificate="12A34B567890123ABCD4EF567A8" \<!-- El certificado que se debe usar en el asistente. -->  
  
            -   Subscription="1a2b34c5-67d8-90ef-ab12-xxxxxxxxxxxxx" \<!-- La suscripción que se debe usar en el asistente. -->  
  
            -   Name="Mi suscripción" \<! -- El nombre de la suscripción. -->  
  
            -   Publisher="" />  
  
    -   \</DeploymentSettings>  
  
 **Valores del archivo de configuración**  
  
###  <a name="permissions"></a> Permissions  
 La base de datos que se implementa debe estar en un estado normal, la base de datos debe ser accesible para la cuenta de usuario que ejecuta el asistente y la cuenta de usuario debe tener permisos para realizar una operación de copia de seguridad.  
  
##  <a name="launch_wizard"></a> Con el Asistente para implementar base de datos en la VM de Microsoft Azure  
 **Para iniciar el asistente, realice los pasos siguientes:**  
  
1.  Use SQL Server Management Studio para conectarse a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con la base de datos que desea implementar.  
  
2.  En el **Explorador de objetos**, expanda el nombre de instancia y, a continuación, expanda el nodo **Bases de datos** .  
  
3.  Haga clic con el botón derecho en la base de datos que desea implementar, seleccione **Tarea**y, luego, seleccione **Implementar base de datos en una VM de Microsoft Azure**.  
  
##  <a name="wizard_pages"></a> Páginas del asistente  
 Las secciones siguientes proporcionan información adicional sobre la configuración de implementación y detalles de configuración para esta operación.  
  
-   [Introducción](#Introduction)  
  
-   [Configuración de origen](#Source_settings)  
  
-   [Inicio de sesión en Windows Azure](#Azure_sign-in)  
  
-   [Configuración de implementación](#Deployment_settings)  
  
-   [Resumen](#Summary)  
  
-   [Resultado](#Results)  
  
##  <a name="Introduction"></a> Introducción 
 En esta página se describe el asistente para **Implementar una base de datos en una VM de Microsoft Azure** .  
  
-   **No volver a mostrar esta página.**  
  Active esta casilla para que la página Introducción deje de mostrarse en el futuro.  
  
-   **Siguiente**  
Continúa en la página **Configuración de origen** .  
  
-   **Cancelar**  
  Cancela la operación y cierra el asistente.  
  
-   **Ayuda**  
Inicia el tema de Ayuda en MSDN para el asistente.  
  
##  <a name="Source_settings"></a> Configuración de origen  
 Use esta página para conectarse a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda la base de datos que desea implementar en la VM de Microsoft Azure. También especificará una ubicación temporal de la máquina virtual para guardar los archivos antes de que se transfieran a Microsoft Azure. Esta puede ser una ubicación de red compartida.  
 
- **SQL Server**    
Haga clic en **Conectar** y especifique los detalles de conexión para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda la base de datos que se va a implementar.  
  
-   **Seleccionar base de datos**  
Use la lista desplegable para especificar la base de datos que se va a implementar.  
  
-   **Otras configuraciones**  
En el campo, especifique una carpeta compartida que estará accesible para el servicio de VM de Microsoft Azure.  
  
##  <a name="Azure_sign-in"></a> Inicio de sesión en Microsoft Azure  
 Inicie sesión en Microsoft Azure con la cuenta de Microsoft o la cuenta corporativa. La cuenta corporativa o de Microsoft presenta el formato de una dirección de correo electrónico, como patc@contoso.com. Para más información sobre las credenciales de Azure, consulte [Microsoft Account for Organizations FAQ](http://technet.microsoft.com/jj592903) (Preguntas más frecuentes sobre Microsoft - Cuenta para organizaciones) y [Solución de problemas](https://technet.microsoft.com/dn197220).  
  
##  <a name="Deployment_settings"></a> Configuración de implementación
 Use esta página para especificar el servidor de destino y proporcionar detalles sobre la nueva base de datos.  
  
 **Máquina virtual de Microsoft Azure**  
  
-   **Nombre del servicio en la nube**  
Especifique el nombre del servicio que hospeda la máquina virtual. Para crear un nuevo servicio en la nube, especifique un nombre para este.  
  
-   **Nombre de máquina virtual** Especifique el nombre de la máquina virtual que hospedará la base de datos de SQL Server. Para crear una máquina virtual de Microsoft Azure nueva, especifique un nombre para esta.  
  
-   **Cuenta de almacenamiento**  
Seleccione la cuenta de almacenamiento en la lista desplegable. Para crear una nueva cuenta de almacenamiento, especifique un nombre para esta. Observe que las cuentas de almacenamiento asociadas a un grupo de afinidad no estarán disponibles en la lista desplegable.  

-   **Configuración**  
Use el botón Configuración para crear una máquina virtual nueva que hospede la base de datos de SQL Server. Si está utilizando una VM existente, la información que proporcione se utilizará para autenticar las credenciales.  
  
**Base de datos de destino**
  
-   **Nombre de instancia de SQL**  
Detalles de conexión del servidor.  
  
-   **Nombre de la base de datos**  
Especifique o confirme el nombre de una base de datos nueva. Si el nombre de la base de datos ya existe en la instancia de SQL Server de destino, se recomienda especificar un nombre de base de datos modificado.  
  
##  <a name="Summary"></a> Resumen
 Esta página se utiliza para revisar la configuración especificada para la operación. Para completar la operación de implementación con los valores especificados, haga clic en **Finalizar**. Para cancelar la operación de implementación y salir del asistente, haga clic en **Cancelar**.  Si hace clic en **Finalizar** , se abrirá la página **Progreso de la implementación** .  También puede consultar el progreso en el archivo de registro que se encuentra en `"%LOCALAPPDATA%\SQL Server\Deploy to SQL in WA VM"`.
  
 Puede haber pasos manuales que sean necesarios para implementar los detalles de la base de datos en la base de datos de SQL Server en la VM de Windows Azure. Estos pasos se describen en detalle.  
  
##  <a name="Results"></a> Resultado 
 En esta página se notifica la corrección o el error de la operación de implementación, mostrando los resultados de cada acción. Cualquier acción que encuentre un error tendrá una indicación en la columna **Resultado** . Haga clic en el vínculo para ver un informe del error para esa acción.  
  
 Haga clic en **Finalizar** para cerrar el asistente.  
  
## <a name="see-also"></a>Ver también  
 [adaptador para la nube de SQL Server](http://msdn.microsoft.com/library/82ed0d0f-952d-4d49-aa36-3855a3ca9877)   
 [Administración del ciclo de vida de base de datos](../../relational-databases/database-lifecycle-management.md)   
 [Exportar una aplicación de capa de datos](../../relational-databases/data-tier-applications/export-a-data-tier-application.md)   
 [Importar un archivo de bacpac para crear una nueva base de datos de usuario](../../relational-databases/data-tier-applications/import-a-bacpac-file-to-create-a-new-user-database.md)   
 [Copias de seguridad y restauración de bases de datos SQL de Azure](https://msdn.microsoft.com/library/azure/jj650016.aspx)   
 [Implementación de SQL Server en máquinas virtuales de Microsoft Azure](http://msdn.microsoft.com/library/dn133141.aspx)   
 [Preparación para la migración a SQL Server en máquinas virtuales de Microsoft Azure](http://msdn.microsoft.com/library/dn133142.aspx)  
  
  
