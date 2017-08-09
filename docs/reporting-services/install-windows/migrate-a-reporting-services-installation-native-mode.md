---
title: "Migrar una instalación de Reporting Services (modo nativo) | Documentos de Microsoft"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- manual Reporting Services migrations
- Report Server Windows service
- custom Reporting Services installations
- automatic Reporting Services migrations
- Reporting Services, upgrades
- upgrading Reporting Services
- migrating Reporting Services
ms.assetid: a6fc56c1-c504-438d-a2b0-5ed29c24e7d6
caps.latest.revision: 54
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: b1e79ca61f1de78ca82cb65aadccd9ea214090a7
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---

# <a name="migrate-a-reporting-services-installation-native-mode"></a>Migrar una instalación de Reporting Services (modo nativo)

[!INCLUDE[ssrs-appliesto-sql2016-xpreview](../../includes/ssrs-appliesto-sql2016-xpreview.md)]

Este tema proporciona instrucciones paso a paso para migrar una de las siguientes versiones admitidas de un [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] implementación en modo nativo a una nueva instancia de SQL Server Reporting Services:  
  
-   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
-   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
-   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
-   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  

Para obtener más información sobre cómo migrar una implementación en modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , vea [Migrar una instalación de Reporting Services &#40;modo de SharePoint&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md).  
  
 Migración se define como mover los archivos de datos de aplicación a una nueva instancia de SQL Server. A continuación se muestran los motivos comunes para migrar la instalación:  
  
-   Tiene una implementación a gran escala o requisitos de tiempo de actividad.  
  
-   Va a cambiar el hardware o la topología de la instalación.  
  
-   Encontró un problema que bloquea la actualización.

## <a name="bkmk_nativemode_migration_overview"></a> Información general de la migración en modo nativo

 El proceso de migración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] incluye pasos manuales y automatizados. A continuación se exponen las tareas necesarias para la migración de un servidor de informes:  
  
-   Realizar una copia de seguridad de los archivos de configuración, aplicación y base de datos.  
  
-   Realizar una copia de seguridad de la clave de cifrado.  
  
-   Instalar una nueva instancia de SQL Server. Si usas el mismo hardware, puede instalar en paralelo de SQL Server con la instalación existente si era una de las versiones compatibles.  
  
    > [!TIP]  
    >  Una instalación en paralelo puede requerir que instale a SQL Server como una instancia con nombre.  
  
-   Mover la base de datos del servidor de informes y otros archivos de aplicación de una instalación existente a la nueva instalación de SQL Server.  
  
-   Mover los archivos de aplicación personalizados a la instalación nueva.  
  
-   Configurar el servidor de informes.  
  
-   Modificar el archivo **RSReportServer.config** de modo que incluya cualquier configuración personalizada de la instalación anterior.  
  
-   Opcionalmente, configure Listas de control de acceso (ACL) personalizadas para el nuevo grupo de servicios de Windows [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   Quitar las aplicaciones y las herramientas que no se usen después de haber confirmado que la instancia nueva es totalmente operativa.  
  
 Hay restricciones en las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospedan la base de datos del servidor de informes. Revise el tema siguiente si va a volver a usar una base de datos de servidor de informes que se creó en una instalación anterior.  
  
-   [Crear una base de datos del servidor de informes](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md)  
  
##  <a name="bkmk_fixed_database_name"></a> Nombre fijo de la base de datos  
 No se puede cambiar el nombre de la base de datos del servidor de informes. La identidad de la base de datos se registra en los procedimientos almacenados del servidor de informes cuando se crea la base de datos. El cambio del nombre de las bases de datos temporales o principales del servidor de informes hará que se produzcan errores cuando se ejecuten los procedimientos, lo que invalida la instalación del servidor de informes.  
  
 Si el nombre de la base de datos de la instalación existente no es adecuado para la instalación nueva, plantéese la posibilidad de crear una base de datos nueva con el nombre que prefiera y, a continuación, cargar los datos de la aplicación existente mediante las técnicas siguientes:  
  
-   Escriba un script de [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] que llame a los métodos SOAP del servicio web del servidor de informes para copiar datos entre las bases de datos. Para ejecutar el script, puede usar la utilidad RS.exe. Para obtener más información sobre este método, vea [Scripting and PowerShell with Reporting Services (Scripting y PowerShell con Reporting Services)](../../reporting-services/tools/scripting-and-powershell-with-reporting-services.md).  
  
-   Escriba código que llame al proveedor de WMI para copiar datos entre las bases de datos. Para obtener más información sobre este método, vea [Access the Reporting Services WMI Provider (Obtener acceso al proveedor de WMI de Reporting Services)](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md).  
  
-   Si solo tiene unos pocos elementos, puede volver a publicar los informes, los modelos de informe y los orígenes de datos compartidos del Diseñador de informes, del Diseñador de modelos y del Generador de informes en el nuevo servidor de informes. Debe volver a crear asignaciones de roles, suscripciones, programaciones compartidas, calendarios de instantáneas de informes, propiedades personalizadas que establezca en informes u otros elementos, seguridad de elementos de modelo y propiedades que establezca en el servidor de informes. Perderá el historial de informes y los datos del registro de ejecución de informes.  
  
##  <a name="bkmk_before_you_start"></a> Antes de empezar  
 Aunque esté realizando una migración de la instalación en lugar de actualizarla, considere la posibilidad de ejecutar el Asesor de actualizaciones en la instalación existente como ayuda para identificar los problemas que pueden afectar a la migración. Este paso es especialmente útil si está migrando un servidor de informes que no instaló o configuró. Al ejecutar el Asesor de actualizaciones, puede encontrar información sobre una configuración personalizada que podría no admitirse en una nueva instalación de SQL Server.  
  
 Además, debe tener en cuenta varios cambios importantes en SQL Server Reporting Services que afectan a cómo migrar la instalación:
 
- El nuevo [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] reemplazó el Administrador de informes.
  
- A partir de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], IIS ya no es un requisito previo. Si está migrando una instalación del servidor de informes a un equipo nuevo, no necesita agregar el rol de servidor web. Además, los procedimientos para configurar las direcciones URL y la autenticación son diferentes de los de la versión anterior, al igual que las técnicas y las herramientas para diagnosticar y solucionar problemas.  
  
- El servicio web del Servidor de informes, el [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)]y el servicio Windows del Servidor de informes se ejecutan en la misma cuenta. Las tres aplicaciones leen los valores de configuración del archivo RSReportServer.config. 
  
- El [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] y SQL Server Management Studio están diseñados para quitar las características superpuestas. Cada herramienta admite un conjunto distinto de tareas.
  
- Los filtros ISAPI no se admiten en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y versiones posteriores. Si utiliza los filtros ISAPI, debe rediseñar su solución de elaboración de informes antes de la migración.  
  
- Las restricciones de dirección IP no se admiten en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y versiones posteriores. Si utiliza restricciones de dirección IP, debe rediseñar la solución de elaboración de informes antes de la migración o utilizar una tecnología tal como un firewall, un enrutador o Traducción de direcciones de red (NAT) para configurar direcciones que tengan restringido el acceso al servidor de informes.  
  
- Los certificados de cliente de Capa de sockets seguros (SSL) no se admiten en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ni en versiones posteriores. Si utiliza certificados SSL de cliente, debe rediseñar la solución de elaboración de informes antes de la migración.  
  
- Si utiliza un tipo de autenticación distinto de la autenticación integrada de Windows, debe actualizar el elemento `<AuthenticationTypes>` en el archivo **RSReportServer.config** con un tipo de autenticación compatible. Los tipos de autenticación compatibles son NTLM, Kerberos, Negocie y Basic. Las autenticaciones implícita, anónima y .NET Passport no se admiten en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
- Si utiliza hojas de estilos en cascada personalizadas en el entorno de elaboración de informes, no se migrarán. Deberá moverlas manualmente después de la migración.  
  
Para obtener más información acerca de los cambios en SQL Server Reporting Services, consulte la documentación del Asesor de actualizaciones y [What's New in Reporting Services](../../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md).  

## <a name="bkmk_backup"></a> Realizar una copia de seguridad de los archivos y los datos

 Antes de instalar una instancia nueva de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], no olvide hacer una copia de seguridad de todos los archivos de la instalación actual.  
  
1.  Realice una copia de seguridad de la clave de cifrado de la base de datos del servidor de informes. Este paso es esencial para que la migración se realice correctamente. Más adelante en el proceso de migración, debe restaurarla para que el servidor de informes recupere el acceso a los datos cifrados. Para realizar una copia de seguridad de la clave, use el Administrador de configuración de Reporting Services.  
  
2.  Haga una copia de seguridad de la base de datos del servidor de informes mediante uno de los métodos admitidos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, vea las instrucciones sobre cómo hacer una copia de seguridad de la base de datos del servidor de informes en [Mover las bases de datos del servidor de informes a otro equipo &#40;Modo nativo de SSRS&#41;](../../reporting-services/report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md).  
  
3.  Realice una copia de seguridad de los archivos de configuración del servidor de informes. Debe realizar una copia de seguridad de los siguientes archivos:  
  
    1.  RSReportServer.config  
  
    2.  Rswebapplication.config  
  
    3.  Rssvrpolicy.config  
  
    4.  Rsmgrpolicy.config  
  
    5.  Reportingservicesservice.exe.config  
  
    6.  Web.config para el servidor de informes [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] aplicación.  
  
    7.  Machine.config para [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] si lo modificó para las operaciones del servidor de informes.  

## <a name="bkmk_install_ssrs"></a> Instalar SQL Server Reporting Services

 Instale una instancia nueva del servidor de informes en modo de solo archivos para que pueda configurarlo para usar valores no predeterminados. Para realizar una instalación desde la línea de comandos, use el argumento **FilesOnly** . En el Asistente para la instalación, seleccione la opción **Instalar, pero no configurar el servidor**.  
  
 Haga clic en uno de los vínculos siguientes para ver instrucciones sobre cómo instalar una instancia nueva de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]:  
  
-   [Instalación de SQL Server 2016 desde el Asistente para la instalación &#40;programa de instalación&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)  
  
-   [Instalar SQL Server 2016 desde el símbolo del sistema](../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)  

## <a name="bkmk_move_database"></a> Mover la base de datos del servidor de informes

 La base de datos del servidor de informes contiene los informes, modelos, orígenes de datos compartidos, calendarios, recursos, suscripciones y carpetas publicados. También contiene las propiedades de los elementos y del sistema, y los permisos para tener acceso al contenido del servidor de informes.  
  
 Si la migración incluye el uso de una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] diferente, debe mover la base de datos del servidor de informes a la nueva instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] . Si está usando la misma instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] , vaya a la sección [Mover las extensiones o ensamblados personalizados](#bkmk_move_custom).  
  
 Para mover la base de datos del servidor de informes, haga lo siguiente:  
  
1.  Elija la instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] que se va a usar. SQL Server Reporting Services requiere que use una de las siguientes versiones para hospedar la base de datos del servidor de informes:  
  
    -   SQL Server 2016  
  
    -   [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
    -   [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  
  
    -   [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]  
  
    -   [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]  
  
2.  Inicie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y conéctese a [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
3.  Cree la función **RSExecRole** en las bases de datos del sistema si [!INCLUDE[ssDE](../../includes/ssde-md.md)] nunca ha hospedado una base de datos del servidor de informes. Para obtener más información, vea [Crear el RSExecRole](../../reporting-services/security/create-the-rsexecrole.md).  
  
4.  Siga las instrucciones descritas en [Mover las bases de datos del servidor de informes a otro equipo &#40;Modo nativo de SSRS&#41;](../../reporting-services/report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md).  
  
 Recuerde que tanto la base de datos del servidor de informes como la base de datos temporal son interdependientes y deben moverse conjuntamente. No copie las bases de datos; la copia no transfiere todas las configuraciones de seguridad a la nueva instalación. No mueva los trabajos del Agente SQL Server para las operaciones del servidor de informes programadas. El servidor de informes volverá a crear automáticamente estos trabajos.  

## <a name="bkmk_move_custom"></a> Mover las extensiones o ensamblados personalizados

 Si la instalación incluye elementos de informe, ensamblados o extensiones personalizados, debe implementar de nuevo los componentes personalizados. Si no usa componentes personalizados, vaya a la sección [Configurar el servidor de informes](#bkmk_configure_reportserver).  
  
 Para implementar de nuevo los componentes personalizados, haga lo siguiente:  
  
1.  Averigüe los ensamblados son compatibles o si es necesario volver a compilarlos.

    -  Las extensiones de seguridad personalizadas se deben volver a escribir con la interfaz [IAuthenticationExtension2](https://msdn.microsoft.com/library/microsoft.reportingservices.interfaces.iauthenticationextension2.aspx) .
  
    -   Las extensiones de representación personalizadas para [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se deben reescribir con el Modelo de objetos de representación (ROM).  
  
    -   Los representadores OWC HTML y HTML 3.2 no se admiten en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y versiones posteriores.  
  
    -   No debería ser necesario volver a compilar otros ensamblados personalizados.  
  
2.  Mueva los ensamblados en la nueva carpeta de \bin del servidor de informes. En SQL Server, los binarios del servidor de informes se encuentran en la siguiente ubicación para la instancia del servidor de informes de forma predeterminada:  
  
     `\Program files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\ReportServer\bin`  
  
3.  Modifique los archivos de configuración para agregar las entradas del componente personalizado. Las entradas variarán según el tipo de ensamblado que use. Para obtener instrucciones sobre dónde colocar los archivos y agregar las entradas de configuración, vea lo siguiente:  
  
    1.  [Implementar un ensamblado personalizado](../../reporting-services/custom-assemblies/deploying-a-custom-assembly.md)  
  
    2.  [Cómo implementar un elemento de informe personalizado](../../reporting-services/custom-report-items/how-to-deploy-a-custom-report-item.md)  
  
    3.  [Implementar una extensión de procesamiento de datos](../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension.md)  
  
    4.  [Implementar una extensión de entrega](../../reporting-services/extensions/delivery-extension/deploying-a-delivery-extension.md)  
  
    5.  [Implementar una extensión de representación](../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)  
  
    6.  [Implementar una extensión de seguridad](../../reporting-services/extensions/security-extension/implementing-a-security-extension.md)  

## <a name="bkmk_configure_reportserver"></a> Configurar el servidor de informes

 Configure las direcciones URL para el portal de web y servicio Web del servidor de informes y configurar la conexión a la base de datos del servidor de informes.  
  
 Si está migrando una implementación escalada, ponga todos los nodos de servidor de informes sin conexión y migre cada servidor de uno en uno. Una vez que se migra el primer servidor de informes y se conecta correctamente a la base de datos del servidor de informes, la versión de base de datos del servidor de informes se actualiza automáticamente a la versión de la base de datos de SQL Server.  
  
> [!IMPORTANT]  
>  Si cualquiera de los servidores de informes de la implementación escalada está conectado y no se ha migrado, podría encontrar una excepción rsInvalidReportServerDatabase porque esté utilizando un esquema más antiguo al conectarse a los actualizados.  
  
> [!NOTE]  
>  Si el servidor de informes para el que realizó la migración se configuró como base de datos compartida para una implementación escalada, deberá eliminar alguna de las claves de cifrado antiguas de la tabla **Keys** de la base de datos **ReportServer** , antes de configurar el servicio del servidor de informes. Si no se quitan las claves, el servidor de informes migrado intentará inicializarse en modo de implementación escalada. Para obtener más información, vea [Agregar y quitar claves de cifrado para implementaciones escaladas &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/add-and-remove-encryption-keys-for-scale-out-deployment.md) y [Configurar y administrar claves de cifrado &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md).  
>   
>  Las claves de escalamiento no se pueden eliminar utilizando el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Las claves antiguas se deben eliminar de la tabla **Keys** de la base de datos **ReportServer** con SQL Server Management Studio. Elimine todas las filas de la tabla Keys. De esta manera, borrará la tabla y la preparará para restaurar únicamente la clave simétrica, tal y como se documenta en los siguientes pasos.  
>   
>  Antes de eliminar las claves, se recomienda hacer primero una copia de seguridad de la clave de cifrado simétrica. Puede utilizar el Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para hacer una copia de seguridad de la clave. Abra el Administrador de configuración, haga clic en la pestaña **Claves de cifrado** y, a continuación, haga clic en el botón **Copia de seguridad** . También puede crear scripts de comandos WMI para hacer una copia de seguridad de la clave de cifrado. Para obtener más información sobre WMI, vea [Método BackupEncryptionKey &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-backupencryptionkey.md).  
  
1.  Inicie el Administrador de configuración de Reporting Services y conéctese a la instancia recién instalada de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para obtener más información, vea [Administrador de configuración de Reporting Services &#40;modo nativo&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md).  
  
2.  Configurar las direcciones URL para el servidor de informes y el portal web. Para obtener más información, vea [Configurar una dirección URL &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md).  
  
3.  Seleccione la base de datos del servidor de informes existente de la instalación anterior y configúrela. Después de configurar la seguridad, los servicios de servidor de informes se reinician y, una vez que se realiza una conexión a la base de datos del servidor de informes, la base de datos se actualizarán automáticamente a SQL Server Reporting Services. Para obtener más información sobre cómo ejecutar el Asistente de base de datos de cambio que usa para crear o seleccionar una base de datos del servidor de informes, consulte [crear una base de datos de servidor de informes de modo nativo](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md).  
  
4.  Restaure las claves de cifrado. Este paso es necesario para habilitar el cifrado reversible en las cadenas de conexión ya existentes y las credenciales que ya están en la base de datos del servidor de informes. Para obtener más información, vea [Hacer copia de seguridad y restaurar claves de cifrado de Reporting Services](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md).  
  
5.  Si instaló el servidor de informes en un equipo nuevo y usa el Firewall de Windows, asegúrese de que el puerto TCP en el que escuche el servidor de informes esté abierto. De forma predeterminada, este puerto es el 80. Para obtener más información, vea [Configurar un firewall para el acceso al servidor de informes](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md).  
  
6.  Si desea administrar el servidor de informes de modo nativo localmente, debe configurar el sistema operativo para permitir la administración local con el portal web. Para obtener más información, consulte [configurar un servidor de informes de modo nativo para la administración Local](../../reporting-services/report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  

## <a name="bkmk_copy_custom_config"></a> Copiar los valores de configuración personalizados en el archivo RSReportServer.config

Si modificó el archivo RSReportServer.config o el archivo RSWebApplication.config en la instalación anterior, debe realizar las mismas modificaciones en el nuevo archivo RSReportServer.config. En la lista siguiente se resume algunas de las razones por las que podría haber modificado el archivo de configuración anterior y proporciona vínculos a información adicional acerca de cómo configurar los mismos valores en SQL Server 2016.  
  
|Personalización|Información|  
|-------------------|-----------------|  
|Entrega de correo electrónico del servidor de informes con los valores de configuración personalizados|[Configuración de correo: modo nativo de](../../reporting-services/install-windows/e-mail-settings-reporting-services-native-mode-configuration-manager.md).|  
|Valores de configuración de la información del dispositivo|[Personalizar los parámetros de extensión de representación en RSReportServer.Config](../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)|

## <a name="bkmk_windowsservice_group"></a> Grupo de servicios de Windows y ACL de seguridad

 En [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)], hay un grupo de servicios, el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] grupo de servicios de Windows, que se utiliza para crear las ACL de seguridad para todas las claves del registro, archivos y carpetas que se instalan con SQL Server Reporting Services. Este nombre de grupo de Windows aparece en el formato SQLServerReportServerUser$\<*computer_name*>$\<*instance_name*>.  

## <a name="bkmk_verify"></a> Comprobar la implementación

1.  Compruebe los directorios virtuales del servido de informes y del [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)] ; para ello, abra un explorador y escriba la dirección URL. Para obtener más información, vea [Comprobar una instalación de Reporting Services](../../reporting-services/install-windows/verify-a-reporting-services-installation.md).  
  
2.  Compruebe los informes para ver si contienen los datos esperados. Revise la información del origen de datos para ver si todavía está especificada la información de conexión del origen de datos. El servidor de informes usa el modelo de objetos de informe al procesar y representar los informes, pero no las reemplaza [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] construye con elementos nuevos del lenguaje de definición de informe. Para obtener más información acerca de cómo los informes existentes se ejecutan en una nueva versión de su servidor de informes, vea [Upgrade Reports](../../reporting-services/install-windows/upgrade-reports.md).  

## <a name="bkmk_remove_unused"></a> Quitar los programas y archivos que no se usan

Cuando haya migrado correctamente el servidor de informes a una nueva instancia, puede realizar los pasos siguientes para quitar los programas y archivos que ya no son necesarios.  
  
1.  Desinstale la versión anterior de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] si ya no la necesita. Este paso no elimina los elementos siguientes, pero puede quitarlos manualmente si ya no los necesita:  
  
    -   La antigua base de datos del servidor de informes  
  
    -   Rol RsExec  
  
    -   Cuentas de servicio del servidor de informes  
  
    -   Grupo de aplicaciones para el servicio web del servidor de informes.  
  
    -   Directorios virtuales para el Administrador de informes y el servidor de informes  
  
    -   Archivos de registro del servidor de informes  
  
2.  Quite IIS si ya no lo necesita en este equipo.

## <a name="next-steps"></a>Pasos siguientes

[Migrar una instalación de Reporting Services](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md)   
[Base de datos de servidor de informes](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)   
[Actualizar y migrar Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)   
[Compatibilidad con versiones anteriores de Reporting Services](../../reporting-services/reporting-services-backward-compatibility.md)   
[Administrador de configuración de Reporting Services](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)  

¿Más preguntas? [Pruebe a formular el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
