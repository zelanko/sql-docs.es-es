---
title: Miembros de MSReportServer_ConfigurationSetting | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- MSReportServer_ConfigurationSetting Members
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- WMI provider [Reporting Services], MSReportServer_ConfigurationSetting class
- MSReportServer_ConfigurationSetting class
ms.assetid: 5e21a53a-a2f8-4b35-a8d9-5483519e3857
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: df662a1ecfe70b9a28eff3947dee4aa769ef2506
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66097311"
---
# <a name="msreportserverconfigurationsetting-members"></a>Miembros MSReportServer_ConfigurationSetting
  La clase MSReportServer_ConfigurationSetting contiene los siguientes métodos y propiedades.  
  
## <a name="public-properties"></a>Propiedades públicas  
  
|||  
|-|-|  
|[ConnectionPoolSize](configurationsetting-property-connectionpoolsize.md)|Devuelve el tamaño de grupo de conexiones usado por el servidor de informes para comunicarse con la instancia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] que hospeda la base de datos del servidor de informes. Solo lectura.|  
|[DatabaseLogonAccount](configurationsetting-property-databaselogonaccount.md)|Especifica la cuenta de inicio de sesión usada por el servidor de informes para conectarse a la instancia del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] instance that hosts the report server database. Solo lectura.|  
|[DatabaseLogonTimeout](configurationsetting-property-databaselogontimeout.md)|Especifica el número de segundos de espera antes de que se produzca un error al intentar iniciar sesión en la base de datos del servidor de informes. Solo lectura.|  
|[DatabaseLogonType](configurationsetting-property-databaselogontype.md)|Especifica si el servidor de informes utiliza una cuenta del servicio de Windows, una cuenta de usuario de Windows o un inicio de sesión [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para tener acceso a la base de datos del servidor de informes. Solo lectura.|  
|[DatabaseName](configurationsetting-property-databasename.md)|Especifica el nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda las bases de datos del servidor de informes.|  
|[DatabaseQueryTimeout](configurationsetting-property-databasequerytimeout.md)|Especifica el número de segundos que deben transcurrir antes de que se agote el tiempo de espera del comando o se produzca un error. El servidor de informes está sincronizando el proceso con respecto a la base de datos del servidor de informes, no un origen de datos para el informe.|  
|[DatabaseServerName](configurationsetting-property-databaseservername.md)|Especifica el nombre del servidor en el que está instalada la base de datos del servidor de informes.|  
|[Propiedad InstallationID](configurationsetting-property-installationid.md)|Devuelve un identificador único para una instancia del servidor de informes concreta.|  
|[InstanceName](configurationsetting-property-instancename.md)|Especifica el nombre de una instancia del servidor de informes en un equipo específico.|  
|[IsInitialized](configurationsetting-property-isinitialized.md)|Indica si se ha inicializado la instancia del servidor de informes. Solo lectura.|  
|[IsSharePointIntegrated](configurationsetting-property-issharepointintegrated.md)|Indica si el servidor de informes se ha configurado para el modo integrado de SharePoint.|  
|[IsWebServiceEnabled](configurationsetting-property-iswebserviceenabled.md)|Indica si el servicio web del servidor de informes está habilitado. Solo lectura.|  
|[IsWindowsServiceEnabled](configurationsetting-property-iswindowsserviceenabled.md)|Indica si el servicio Servidor de informes de Windows está habilitado. Solo lectura.|  
|[Propiedad MachineAccountIdentity &#40;WMI&#41;](configurationsetting-property-machineaccountidentity.md)|Obtiene la identidad de la cuenta del equipo en el que está instalado el servidor de informes.|  
|[PathName](configurationsetting-property-pathname.md)|Especifica la ruta de instalación a una instancia del servidor de informes.|  
|[SecureConnectionLevel](configurationsetting-property-secureconnectionlevel.md)|Devuelve el nivel de conexión segura especificado en el archivo RSReportServer.config.|  
|[SenderEmailAddress](configurationsetting-property-senderemailaddress.md)|Obtiene la dirección utilizada para enviar el correo electrónico desde el servidor de informes. Solo lectura.|  
|[SendUsingSMTPServer](configurationsetting-property-sendusingsmtpserver.md)|Especifica si la propiedad SendUsing en la configuración del correo electrónico está establecida en TRUE.|  
|[SMTPServer](configurationsetting-property-smtpserver.md)|Obtiene la propiedad de servidor SMTP a partir del archivo RSReportServer.config. Solo lectura.|  
|[UnattendedExecutionAccount](configurationsetting-property-unattendedexecutionaccount.md)|Especifica la cuenta de usuario de inicio de sesión que el servidor de informes suplanta al ejecutarse los informes de forma desatendida. Solo lectura.|  
|[Versión](configurationsetting-property-version.md)|Devuelve la versión del servidor de informes.|  
|[Propiedad VirtualDirectoryReportManager &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-property-virtualdirectoryreportmanager.md)|Devuelve el directorio virtual para la aplicación de administrador de informes.|  
|[Propiedad VirtualDirectoryReportServer &#40;MSReportServer_ConfigurationSetting de WMI&#41;](configurationsetting-property-virtualdirectoryreportserver.md)|Devuelve el directorio virtual para la aplicación de servicio web del servidor de informes.|  
|[WindowsServiceIdentityActual](configurationsetting-property-windowsserviceidentityactual.md)|Devuelve la identidad en la que se ejecuta en la actualidad el servicio de Windows de servidor de informes. Solo lectura.|  
|[WindowsServiceIdentityConfigured](windowsserviceidentityconfigured-property.md)|Devuelve la última identidad en la que se configuró el servicio Servidor de informes de Windows para ejecutarse. Solo lectura.|  
  
## <a name="public-methods"></a>Métodos públicos  
  
|||  
|-|-|  
|[BackupEncryptionKey](configurationsetting-method-backupencryptionkey.md)|Realiza una copia de seguridad de la clave de cifrado de la instancia. La clave de cifrado se almacena cifrada con una contraseña.|  
|[Método CreateSSLCertificateBinding &#40;MSReportServer_ConfigurationSetting de WMI&#41;](configurationsetting-method-createsslcertificatebinding.md)|Crea un enlace de certificado SSL.|  
|[DeleteEncryptedInformation](configurationsetting-method-deleteencryptedinformation.md)|Elimina la información cifrada de la base de datos del servidor de informes.|  
|[DeleteEncryptionKey](configurationsetting-method-deleteencryptionkey.md)|Elimina las claves de cifrado de la base de datos del servidor de informes.|  
|[GenerateDatabaseCreationScript](configurationsetting-method-generatedatabasecreationscript.md)|Genera un script SQL que se puede utilizar para crear la base de datos del servidor de informes.|  
|[GenerateDatabaseRightsScript](configurationsetting-method-generatedatabaserightsscript.md)|Genera un script SQL que se puede utilizar para conceder permisos de usuario a la base de datos del servidor de informes.|  
|[GenerateDatabaseUpgradeScript](configurationsetting-method-generatedatabaseupgradescript.md)|Genera un script SQL que se puede utilizar para actualizar una base de datos del servidor de informes.|  
|[Método GetAdminSiteUrl &#40;WMI&#41;](configurationsetting-method-getadminsiteurl.md)|Obtiene la dirección URL absoluta al sitio web de administración central.|  
|[GetDatabaseVersionDisplayName](configurationsetting-method-getdatabaseversiondisplayname.md)|Obtiene el nombre para mostrar para una cadena de versión de base de datos del servidor de informes determinada.|  
|[InitializeReportServer](configurationsetting-method-initializereportserver.md)|Inicializa la instancia del servidor de informes especificada.|  
|[Método ListInstalledSharePointVersions &#40;WMI&#41;](configurationsetting-method-listinstalledsharepointversions.md)|Devuelve un conjunto de tokens que representan las versiones de [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)], or [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] que se instalan en el mismo equipo que el servidor de informes.|  
|[Método ListIPAddresses &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-listipaddresses.md)|Enumera las direcciones IP del equipo.|  
|[ListReportServersInDatabase](configurationsetting-method-listreportserversindatabase.md)|Devuelve una lista de las instalaciones del servidor de informes que se encuentran en la base de datos del servidor de informes, sin tener en cuenta si esas instalaciones tienen acceso a la información segura.|  
|[Método ListReservedURLs &#40;MSReportServer_ConfigurationSetting de WMI&#41;](configurationsetting-method-listreservedurls.md)|Enumera las direcciones URL reservadas para todas las aplicaciones en el servidor de informes.|  
|[Método ListSSLCertificateBindings &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-listsslcertificatebindings.md)|Enumera los enlaces de certificados SSL que existen en HTTP.SYS y los esperados a partir de rsreportserver.config.|  
|[Método ListSSLCertificates &#40;WMI MSReportServer_ConfigurationSetting&#41;](configurationsetting-method-listsslcertificates.md)|Enumera los certificados SSL instalados en el equipo.|  
|[ReencryptSecureInformation](configurationsetting-method-reencryptsecureinformation.md)|Genera una nueva clave de cifrado y vuelve a cifrar toda la información segura en la base de datos del servidor de informes utilizando esta nueva clave.|  
|[Método RemoveSSLCertificateBindings &#40;MSReportServer_ConfigurationSetting de WMI&#41;](configurationsetting-method-removesslcertificatebinding.md)|Quita un enlace de certificado SSL.|  
|[RemoveUnattendedExecutionAccount](configurationsetting-method-removeunattendedexecutionaccount.md)|Elimina la entrada de cuenta de ejecución desatendida de la configuración del servidor de informes.|  
|[Método RemoveURL &#40;MSReportServer_ConfigurationSetting de WMI&#41;](configurationsetting-method-removeurl.md)|Quita una dirección URL reservada para el servidor de informes.|  
|[Método ReserveURL &#40;MSReportServer_ConfigurationSetting de WMI&#41;](configurationsetting-method-reserveurl.md)|Agrega una reserva URL para una aplicación determinada.|  
|[RestoreEncryptionKey](configurationsetting-method-restoreencryptionkey.md)|Vuelve a aplicar la clave de cifrado especificada a la base de datos del servidor de informes.|  
|[SetDatabaseConnection](configurationsetting-method-setdatabaseconnection.md)|Define la conexión de la base de datos del servidor de informes a una base de datos de servidor de informes concreta.|  
|[SetDatabaseLogonTimeout](configurationsetting-method-setdatabaselogontimeout.md)|Especifica el valor de tiempo de espera predeterminado para los intentos de inicio de sesión de la base de datos del servidor de informes.|  
|[SetDatabaseQueryTimeout](configurationsetting-method-setdatabasequerytimeout.md)|Especifica el valor de tiempo de espera predeterminado para las conexiones de la base de datos del servidor de informes.|  
|[SetEmailConfiguration](configurationsetting-method-setemailconfiguration.md)|Configura la extensión de entrega de correo electrónico utilizada por el servidor de informes para enviar el correo electrónico.|  
|[SetSecureConnectionLevel](configurationsetting-method-setsecureconnectionlevel.md)|Establece el nivel de conexión segura del servidor de informes.|  
|[SetServiceState](configurationsetting-method-setservicestate.md)|Activa y desactiva los servicios web y los servicios del Servidor de informes de Windows.|  
|[SetUnattendedExecutionAccount](configurationsetting-method-setunattendedexecutionaccount.md)|Especifica la cuenta utilizada para ejecutar informes de forma desatendida.|  
|[Método SetVirtualDirectory &#40;MSReportServer_ConfigurationSetting de WMI&#41;](configurationsetting-method-setvirtualdirectory.md)|Establece el directorio virtual para una aplicación.|  
|[SetWindowsServiceIdentity](configurationsetting-method-setwindowsserviceidentity.md)|Hace que el servicio Windows del servidor de informes se ejecute como el usuario de Windows especificado y concede a esta cuenta suficientes permisos de sistema de archivos para que el servidor de informes pueda funcionar.|  
  
## <a name="see-also"></a>Vea también  
 [MSReportServer_ConfigurationSetting Class](msreportserver-configurationsetting-class.md)  
  
  
