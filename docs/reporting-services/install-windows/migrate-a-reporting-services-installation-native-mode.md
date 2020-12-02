---
description: Migrar una instalación de Reporting Services (modo nativo)
title: Migrar una instalación de Reporting Services (modo nativo) | Microsoft Docs
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
ms.date: 05/01/2020
ms.openlocfilehash: ae3932611181f99b71d72bc2365967a19c968b9c
ms.sourcegitcommit: f2bdebed3efa55a2b7e64de9d6d9d9b1c85f479e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/24/2020
ms.locfileid: "96125012"
---
# <a name="migrate-a-reporting-services-installation-native-mode"></a>Migrar una instalación de Reporting Services (modo nativo)

En este tema se proporcionan instrucciones paso a paso para migrar una de las siguientes versiones admitidas de una implementación en modo nativo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a una nueva instancia de SQL Server Reporting Services:  
  
::: moniker range=">=sql-server-2017||=sqlallproducts-allversions"
* [!INCLUDE[ssSQL16](../../includes/sssql16-md.md)]

* [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
* [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
* [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
* [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]
::: moniker-end

::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
* [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
* [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
* [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
* [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]

Para obtener más información sobre cómo migrar una implementación en modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , vea [Migrar una instalación de Reporting Services &#40;modo de SharePoint&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md).  

::: moniker-end
  
 La migración se define como la acción de mover los archivos de datos de aplicación a una instancia nueva de SQL Server. A continuación se muestran los motivos comunes para migrar la instalación:  
  
* Tiene una implementación a gran escala o requisitos de tiempo de actividad.  
  
* Va a cambiar el hardware o la topología de la instalación.  
  
* Encontró un problema que bloquea la actualización.

## <a name="native-mode-migration-overview"></a><a name="bkmk_nativemode_migration_overview"></a> Información general de la migración en modo nativo

 El proceso de migración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] incluye pasos manuales y automatizados. A continuación se exponen las tareas necesarias para la migración de un servidor de informes:  
  
* Realizar una copia de seguridad de los archivos de configuración, aplicación y base de datos.  
  
* Realizar una copia de seguridad de la clave de cifrado.  
  
* Instalar una instancia nueva de SQL Server. Si usa el mismo hardware, puede instalar SQL Server en paralelo con la instalación existente si era una de las versiones admitidas.  
  
    > [!TIP]  
    >  Una instalación en paralelo puede requerir que instale SQL Server como una instancia con nombre.
  
* Mover la base de datos del servidor de informes y otros archivos de aplicación de una instalación existente a la nueva instalación de SQL Server.  
  
* Mover los archivos de aplicación personalizados a la instalación nueva.  
  
* Configurar el servidor de informes.  
  
* Modificar el archivo **RSReportServer.config** de modo que incluya cualquier configuración personalizada de la instalación anterior.  
  
* Opcionalmente, configure Listas de control de acceso (ACL) personalizadas para el nuevo grupo de servicios de Windows [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
* Quitar las aplicaciones y las herramientas que no se usen después de haber confirmado que la instancia nueva es totalmente operativa.  
  
 Hay restricciones en las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospedan la base de datos del servidor de informes. Revise el tema siguiente si va a volver a usar una base de datos de servidor de informes que se creó en una instalación anterior.  
  
* [Crear una base de datos del servidor de informes](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md)  
  
## <a name="fixed-database-name"></a><a name="bkmk_fixed_database_name"></a> Nombre fijo de la base de datos

 No se puede cambiar el nombre de la base de datos del servidor de informes. La identidad de la base de datos se registra en los procedimientos almacenados del servidor de informes cuando se crea la base de datos. El cambio del nombre de las bases de datos temporales o principales del servidor de informes hace que se produzcan errores al ejecutar los procedimientos, lo que invalida la instalación del servidor de informes.  
  
 Si el nombre de la base de datos de la instalación existente no es adecuado para la instalación nueva, plantéese la posibilidad de crear una base de datos nueva con el nombre que prefiera y, a continuación, cargar los datos de la aplicación existente mediante las técnicas siguientes:  
  
* Escriba un script de [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] que llame a los métodos SOAP del servicio web del servidor de informes para copiar datos entre las bases de datos. Para ejecutar el script, puede usar la utilidad RS.exe. Para obtener más información sobre este método, vea [Scripting and PowerShell with Reporting Services (Scripting y PowerShell con Reporting Services)](../../reporting-services/tools/scripting-and-powershell-with-reporting-services.md).  
  
* Escriba código que llame al proveedor de WMI para copiar datos entre las bases de datos. Para obtener más información sobre este método, vea [Access the Reporting Services WMI Provider (Obtener acceso al proveedor de WMI de Reporting Services)](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md).  
  
* Si solo tiene unos pocos elementos, puede volver a publicar los informes y los orígenes de datos compartidos del Diseñador de informes, del Diseñador de modelos y del Generador de informes en el nuevo servidor de informes. Vuelva a crear las asignaciones de roles, suscripciones, programaciones compartidas, calendarios de instantáneas de informes, propiedades personalizadas que establezca en informes u otros elementos, seguridad de elementos de modelo y propiedades que establezca en el servidor de informes. Prepárese para perder el historial de informes y los datos del registro de ejecución de informes si sigue estas acciones.
  
## <a name="before-you-start"></a><a name="bkmk_before_you_start"></a> Antes de empezar

 Aunque esté realizando una migración de la instalación en lugar de actualizarla, considere la posibilidad de ejecutar el Asesor de actualizaciones en la instalación existente como ayuda para identificar los problemas que pueden afectar a la migración. Este paso es especialmente útil si está migrando un servidor de informes que no instaló o configuró. Al ejecutar el Asesor de actualizaciones, puede descubrir valores personalizados que quizás no se admitan en una instalación nueva de SQL Server.  
  
 Además, debe tener en cuenta varios cambios importantes en SQL Server Reporting Services que afectan al modo de migrar la instalación:

* El nuevo [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] reemplazó el Administrador de informes.
  
* A partir de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], IIS ya no es un requisito previo. Si está migrando una instalación del servidor de informes a un equipo nuevo, no necesita agregar el rol de servidor web. Además, los procedimientos para configurar las direcciones URL y la autenticación son diferentes de los de la versión anterior, al igual que las técnicas y las herramientas para diagnosticar y solucionar problemas.  
  
* El servicio web del Servidor de informes, el [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]y el servicio Windows del Servidor de informes se ejecutan en la misma cuenta. Las tres aplicaciones leen los valores de configuración del archivo RSReportServer.config.
  
* El [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] y SQL Server Management Studio están diseñados para quitar las características superpuestas. Cada herramienta admite un conjunto distinto de tareas.
  
* Los filtros ISAPI no se admiten en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y versiones posteriores. Si utiliza los filtros ISAPI, debe rediseñar su solución de elaboración de informes antes de la migración.  
  
* Las restricciones de dirección IP no se admiten en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y versiones posteriores. Si utiliza restricciones de dirección IP, debe rediseñar la solución de elaboración de informes antes de la migración o utilizar una tecnología tal como un firewall, un enrutador o Traducción de direcciones de red (NAT) para configurar direcciones que tengan restringido el acceso al servidor de informes.  
  
* Los certificados de Seguridad de la capa de transporte (TLS), conocida anteriormente como Capa de sockets seguros (SSL), no se admiten en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y versiones posteriores. Si utiliza certificados TLS de cliente, debe rediseñar la solución de elaboración de informes antes de la migración.  
  
* Si usa un tipo de autenticación distinto de la autenticación integrada de Windows, debe actualizar el elemento `<AuthenticationTypes>` en el archivo **RSReportServer.config** con un tipo de autenticación compatible. Los tipos de autenticación compatibles son NTLM, Kerberos, Negocie y Basic. Las autenticaciones implícita, anónima y .NET Passport no se admiten en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ni en versiones posteriores.  
  
* Si usa hojas de estilo CSS personalizadas en el entorno de elaboración de informes, no se podrán migrar. Muévalas manualmente después de la migración.
  
Para obtener más información sobre los cambios en SQL Server Reporting Services, vea la documentación del Asesor de actualizaciones y [Novedades de Reporting Services &#40;SSRS&#41;](../../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md).  

## <a name="backup-files-and-data"></a><a name="bkmk_backup"></a> Realizar una copia de seguridad de los archivos y los datos

 Antes de instalar una instancia nueva de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], no olvide hacer una copia de seguridad de todos los archivos de la instalación actual.  
  
1. Realice una copia de seguridad de la clave de cifrado de la base de datos del servidor de informes. Este paso es esencial para que la migración se realice correctamente. Más adelante en el proceso de migración, debe restaurarla para que el servidor de informes recupere el acceso a los datos cifrados. Para realizar una copia de seguridad de la clave, use el Administrador de configuración del servidor de informes.  
  
2. Haga una copia de seguridad de la base de datos del servidor de informes mediante uno de los métodos admitidos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información, vea las instrucciones sobre cómo hacer una copia de seguridad de la base de datos del servidor de informes en [Mover las bases de datos del servidor de informes a otro equipo &#40;Modo nativo de SSRS&#41;](../../reporting-services/report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md).  
  
3. Realice una copia de seguridad de los archivos de configuración del servidor de informes. Debe realizar una copia de seguridad de los siguientes archivos:  
  
    1. RSReportServer.config  
  
    2. Rswebapplication.config  
  
    3. Rssrvpolicy.config  
  
    4. Rsmgrpolicy.config  
  
    5. Reportingservicesservice.exe.config  
  
    6. Web.config para la aplicación [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] del servidor de informes.  
  
    7. Machine.config para [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] si lo modificó para las operaciones del servidor de informes.  

## <a name="install-sql-server-reporting-services"></a><a name="bkmk_install_ssrs"></a> Instalar SQL Server Reporting Services

 Instale una instancia nueva del servidor de informes en modo de solo archivos para que pueda configurarlo para usar valores no predeterminados. Para realizar una instalación desde la línea de comandos, use el argumento **FilesOnly**. En el Asistente para la instalación, seleccione la opción **Instalar, pero no configurar el servidor**.  
  
 Haga clic en uno de los vínculos siguientes para ver instrucciones sobre cómo instalar una instancia nueva de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]:  
  
* [Instalación de Microsoft SQL Server Reporting Services 2016 y versiones anteriores desde el Asistente para instalación (programa de instalación)](install-reporting-services-native-mode-report-server.md) 
  
* [Instalación de Microsoft SQL Server Reporting Services 2016 y versiones anteriores desde el símbolo del sistema](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)  

* [Instalación de Microsoft SQL Server Reporting Services 2017 y versiones posteriores](install-reporting-services.md)

## <a name="move-the-report-server-database"></a><a name="bkmk_move_database"></a> Mover la base de datos del servidor de informes

 La base de datos del servidor de informes contiene los informes, modelos, orígenes de datos compartidos, calendarios, recursos, suscripciones y carpetas publicados. También contiene las propiedades de los elementos y del sistema, y los permisos para tener acceso al contenido del servidor de informes.  
  
 Si la migración incluye el uso de una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] diferente, debe mover la base de datos del servidor de informes a la nueva instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Si está usando la misma instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] , vaya a la sección [Mover las extensiones o ensamblados personalizados](#bkmk_move_custom).  
  
 Para mover la base de datos del servidor de informes, siga estos pasos:
  
1. Elija la instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] que se va a usar. SQL Server Reporting Services requiere que use una de las siguientes versiones para hospedar la base de datos del servidor de informes:  
  
    ::: moniker range="=sql-server-2017||=sqlallproducts-allversions"
    * [!INCLUDE[ssSQL16](../../includes/sssql16-md.md)]

    * [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
    * [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
    * [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
    * [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]
    ::: moniker-end

    ::: moniker range="=sql-server-2016||=sqlallproducts-allversions"
    * [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  

    * [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  

    * [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  

    * [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]
    ::: moniker-end
  
2. Inicie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y conéctese a [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
3. Cree la función **RSExecRole** en las bases de datos del sistema si [!INCLUDE[ssDE](../../includes/ssde-md.md)] nunca ha hospedado una base de datos del servidor de informes. Para obtener más información, vea [Crear el RSExecRole](../../reporting-services/security/create-the-rsexecrole.md).  
  
4. Siga las instrucciones descritas en [Mover las bases de datos del servidor de informes a otro equipo &#40;Modo nativo de SSRS&#41;](../../reporting-services/report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md).  
  
 Recuerde que tanto la base de datos del servidor de informes como la base de datos temporal son interdependientes y deben moverse conjuntamente. No copie las bases de datos; la copia no transfiere todas las configuraciones de seguridad a la nueva instalación. No mueva los trabajos del Agente SQL Server para las operaciones del servidor de informes programadas. El servidor de informes vuelve a crear estos trabajos de forma automática.  

## <a name="move-custom-assemblies-or-extensions"></a><a name="bkmk_move_custom"></a> Mover las extensiones o ensamblados personalizados

 Si la instalación incluye elementos de informe, ensamblados o extensiones personalizados, debe implementar de nuevo los componentes personalizados. Si no usa componentes personalizados, vaya a la sección [Configurar el servidor de informes](#bkmk_configure_reportserver).  
  
 Para volver a implementar los componentes personalizados, siga estos pasos:  
  
1. Averigüe los ensamblados son compatibles o si es necesario volver a compilarlos.

    * Las extensiones de seguridad personalizadas se deben volver a escribir con la interfaz [IAuthenticationExtension2](/dotnet/api/microsoft.reportingservices.interfaces.iauthenticationextension2).
  
    * Las extensiones de representación personalizadas para [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se deben reescribir con el Modelo de objetos de representación (ROM).  
  
    * Los representadores OWC HTML y HTML 3.2 no se admiten en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ni en versiones posteriores.  
  
    * No debería ser necesario volver a compilar otros ensamblados personalizados.  
  
2. Mueva los ensamblados a la nueva carpeta \bin del servidor de informes. En SQL Server, los archivos binarios del servidor de informes se encuentran en la siguiente ubicación para la instancia predeterminada del servidor de informes:  
  
     `\Program files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer\bin`  
  
3. Modifique los archivos de configuración para agregar las entradas del componente personalizado. Las entradas varían según el tipo de ensamblado que use. Para obtener instrucciones sobre dónde colocar los archivos y agregar las entradas de configuración, vea lo siguiente:  
  
    1. [Implementación de un ensamblado personalizado](../../reporting-services/custom-assemblies/deploying-a-custom-assembly.md)  
  
    2. [Cómo: Implementar un elemento de informe personalizado](../../reporting-services/custom-report-items/how-to-deploy-a-custom-report-item.md)  
  
    3. [Implementación de una extensión de procesamiento de datos](../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)  
  
    4. [Implementación de una extensión de entrega](../../reporting-services/extensions/delivery-extension/deploying-a-delivery-extension.md)  
  
    5. [Implementación de una extensión de representación](../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)  
  
    6. [Implementación de una extensión de seguridad](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)  

## <a name="configure-the-report-server"></a><a name="bkmk_configure_reportserver"></a> Configurar el servidor de informes

 Configure las direcciones URL para el servicio web del servidor de informes y el portal web, y configure la conexión con la base de datos del servidor de informes.  
  
 Si está migrando una implementación escalada, ponga todos los nodos de servidor de informes sin conexión y migre cada servidor de uno en uno. Una vez que el primer servidor de informes se haya migrado y conectado correctamente a la base de datos del servidor de informes, la versión de la base de datos del servidor de informes se actualizará automáticamente a la versión de base de datos de SQL Server.  
  
> [!IMPORTANT]
>  Si cualquiera de los servidores de informes de la implementación escalada está en línea y no se ha migrado, podría encontrar una excepción *rsInvalidReportServerDatabase* porque use un esquema más antiguo al conectarse a los actualizados.  

Si el servidor de informes que se ha migrado está configurado como la base de datos compartida para una implementación escalada, tendrá que eliminar todas las claves de cifrado antiguas de la tabla **Claves** de la base de datos **ReportServer**, antes de configurar el servicio del servidor de informes. Si no se quitan las claves, el servidor de informes migrado intentará inicializarse en modo de implementación escalada. Para obtener más información, vea [Agregar y quitar claves de cifrado para implementaciones escaladas &#40;Administrador de configuración del servidor de informes&#41;](../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md) y [Configurar y administrar claves de cifrado &#40;Administrador de configuración del servidor de informes&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md).  

Las claves de escalamiento no se pueden eliminar utilizando el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Las claves antiguas se deben eliminar de la tabla **Keys** de la base de datos **ReportServer** con SQL Server Management Studio. Elimine todas las filas de la tabla Keys. Esta acción borra la tabla y la prepara para restaurar únicamente la clave simétrica, como se documenta en los pasos siguientes.  

Antes de eliminar las claves, se recomienda hacer primero una copia de seguridad de la clave de cifrado simétrica. Puede utilizar el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para hacer una copia de seguridad de la clave. Abra Configuration Manager, haga clic en la pestaña Claves de cifrado y, después, haga clic en el botón **Copia de seguridad** . También puede crear scripts de comandos WMI para hacer una copia de seguridad de la clave de cifrado. Para obtener más información sobre WMI, vea [Método BackupEncryptionKey &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-backupencryptionkey.md).  
  
1. Inicie el Administrador de configuración del servidor de informes y conéctese a la instancia de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que ha instalado. Para más información, vea [Administrador de configuración del servidor de informes &#40;modo nativo&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md).  
  
2. Configure las direcciones URL del servidor de informes y el portal web. Para más información, vea [Configurar una dirección URL &#40;Administrador de configuración del servidor de informes&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md).  
  
3. Seleccione la base de datos del servidor de informes existente de la instalación anterior y configúrela. Si la configuración se realiza correctamente, los servicios del servidor de informes se reinician y, una vez realizada la conexión a la base de datos del servidor de informes, la base de datos se actualiza de forma automática a SQL Server Reporting Services. Para obtener más información sobre cómo ejecutar el Asistente para cambiar bases de datos que se usa para crear o seleccionar una base de datos del servidor de informes, vea [Crear una base de datos del servidor de informes de modo nativo](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md).  
  
4. Restaure las claves de cifrado. Este paso es necesario para habilitar el cifrado reversible en las cadenas de conexión ya existentes y las credenciales que ya están en la base de datos del servidor de informes. Para obtener más información, vea [Hacer copia de seguridad y restaurar claves de cifrado de Reporting Services](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md).  
  
5. Si instaló el servidor de informes en un equipo nuevo y usa el Firewall de Windows, asegúrese de que el puerto TCP en el que escuche el servidor de informes esté abierto. De forma predeterminada, este puerto es el 80. Para obtener más información, vea [Configurar un firewall para el acceso al servidor de informes](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md).  
  
6. Si quiere administrar el servidor de informes en modo nativo localmente, necesita configurar el sistema operativo para permitir la administración local con el portal web. Para obtener más información, vea [Configurar un servidor de informes en modo nativo para la administración local](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  

## <a name="copy-custom-configuration-settings-to-rsreportserverconfig-file"></a><a name="bkmk_copy_custom_config"></a> Copiar los valores de configuración personalizados en el archivo RSReportServer.config

Si modificó el archivo RSReportServer.config o el archivo RSWebApplication.config en la instalación anterior, debe realizar las mismas modificaciones en el nuevo archivo RSReportServer.config. En la lista siguiente se resumen algunas de las razones por las que podría haber tenido que modificar el archivo de configuración anterior y se proporcionan vínculos a información adicional sobre cómo configurar los mismos valores en SQL Server 2016.  
  
|Personalización|Information|  
|-------------------|-----------------|  
|Entrega de correo electrónico del servidor de informes con los valores de configuración personalizados|[Configuración de correo electrónico * Modo nativo de Reporting Services](../../reporting-services/install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md).|  
|Valores de configuración de la información del dispositivo|[Personalización de los parámetros de extensión de representación en RSReportServer.Config](../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)|

## <a name="windows-service-group-and-security-acls"></a><a name="bkmk_windowsservice_group"></a> Grupo de servicios de Windows y ACL de seguridad

 En [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] hay un grupo de servicios, el grupo de servicios [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] de Windows, que se usa para crear listas de control de acceso (ACL) de seguridad para todas las claves del Registro, archivos y carpetas que se instalan con SQL Server Reporting Services. Este nombre de grupo de Windows aparece en el formato SQLServerReportServerUser$\<*computer_name*>$\<*instance_name*>.  

## <a name="verify-your-deployment"></a><a name="bkmk_verify"></a> Comprobar la implementación

1. Compruebe los directorios virtuales del servido de informes y del [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] ; para ello, abra un explorador y escriba la dirección URL. Para obtener más información, vea [Comprobar una instalación de Reporting Services](../../reporting-services/install-windows/verify-a-reporting-services-installation.md).  
  
2. Compruebe los informes para ver si contienen los datos esperados. Revise la información del origen de datos para ver si todavía está especificada la información de conexión del origen de datos. El servidor de informes utiliza el modelo de objetos de informe al procesar y representar los informes, pero no reemplaza las construcciones de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] por elementos nuevos del lenguaje de definición de informes (RDL). Para obtener más información sobre cómo se ejecutan los informes existentes en una nueva versión de un servidor de informes , vea [Actualizar informes](../../reporting-services/install-windows/upgrade-reports.md).  

## <a name="remove-unused-programs-and-files"></a><a name="bkmk_remove_unused"></a> Quitar los programas y archivos que no se usan

Una vez que haya migrado correctamente el servidor de informes a una nueva instancia, se recomienda seguir estos pasos para quitar los programas y archivos que ya no sean necesarios.  
  
1. Desinstale la versión anterior de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] si ya no la necesita. Este paso no elimina los elementos siguientes, pero puede quitarlos manualmente si ya no los necesita:  
  
    * La antigua base de datos del servidor de informes  
  
    * Rol RsExec  
  
    * Cuentas de servicio del servidor de informes  
  
    * Grupo de aplicaciones para el servicio web del servidor de informes.  
  
    * Directorios virtuales para el Administrador de informes y el servidor de informes  
  
    * Archivos de registro del servidor de informes  
  
2. Quite IIS si ya no lo necesita en este equipo.

## <a name="next-steps"></a>Pasos siguientes

* [Migrar una instalación de Reporting Services](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md)  
* [Base de datos del servidor de informes](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)   
* [Actualizar y migrar Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
* [Compatibilidad con versiones anteriores de Reporting Services](../../reporting-services/reporting-services-backward-compatibility.md)   
* [Administrador de configuración del servidor de informes](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)  

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).