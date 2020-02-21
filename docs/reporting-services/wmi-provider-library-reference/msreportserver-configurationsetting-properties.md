---
title: Propiedades MSReportServer_ConfigurationSetting | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- MSReportServer_ConfigurationSetting Properties
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- WMI provider [Reporting Services], MSReportServer_ConfigurationSetting class
- MSReportServer_ConfigurationSetting class
ms.assetid: e75fe1e5-197b-4c65-859b-370821cad003
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 634c5065730ea58905f89ac0454cdda53552a126
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "65569095"
---
# <a name="msreportserver_configurationsetting-properties"></a>Propiedades MSReportServer_ConfigurationSetting
  La clase MSReportServer_ConfigurationSetting representa los parámetros de instalación y tiempo de ejecución de una instancia del servidor de informes. La configuración se guarda en el archivo de configuración RSReportServer.config.  
  
## <a name="public-properties"></a>Propiedades públicas  
  
|||  
|-|-|  
|[ConnectionPoolSize](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-connectionpoolsize.md)|Devuelve el tamaño de grupo de conexiones usado por el servidor de informes para comunicarse con la instancia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] que hospeda la base de datos del servidor de informes. Solo lectura.|  
|[DatabaseLogonAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogonaccount.md)|Especifica la cuenta de inicio de sesión usada por el servidor de informes para conectarse a la instancia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] que hospeda la base de datos del servidor de informes. Solo lectura.|  
|[DatabaseLogonTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogontimeout.md)|Especifica el número de segundos de espera antes de que se produzca un error al intentar iniciar sesión en la base de datos del servidor de informes. Solo lectura.|  
|[DatabaseLogonType](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaselogontype.md)|Especifica si el servidor de informes utiliza una cuenta del servicio de Windows, una cuenta de usuario de Windows o un inicio de sesión [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para tener acceso a la base de datos del servidor de informes. Solo lectura.|  
|[DatabaseName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databasename.md)|Especifica el nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda las bases de datos del servidor de informes.|  
|[DatabaseQueryTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databasequerytimeout.md)|Especifica el número de segundos que deben transcurrir antes de que se agote el tiempo de espera del comando o se produzca un error. El servidor de informes está sincronizando el proceso con respecto al catálogo del servidor SQL, no un origen de datos para el informe.|  
|[DatabaseServerName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-databaseservername.md)|Especifica el nombre del servidor en el que está instalada la base de datos del servidor de informes.|  
|[Propiedad InstallationID](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-installationid.md)|Devuelve un identificador único para una instancia del servidor de informes concreta.|  
|[InstanceName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-instancename.md)|Especifica el nombre de una instancia del servidor de informes en un equipo específico.|  
|[IsInitialized](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-isinitialized.md)|Indica si se ha inicializado la instancia del servidor de informes.  Solo lectura.|  
|[IsSharePointIntegrated](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-issharepointintegrated.md)|Indica si el servidor de informes se ha configurado para el modo integrado de SharePoint.|  
|[IsWebServiceEnabled](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-iswebserviceenabled.md)|Indica si el servicio web del servidor de informes está habilitado. Solo lectura.|  
|[IsWindowsServiceEnabled](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-iswindowsserviceenabled.md)|Indica si el servicio Servidor de informes de Windows está habilitado. Solo lectura.|  
|[Propiedad MachineAccountIdentity &#40;WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-machineaccountidentity.md)|Obtiene la identidad de la cuenta del equipo en el que está instalado el servidor de informes.|  
|[PathName](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-pathname.md)|Especifica la ruta de instalación a una instancia del servidor de informes.|  
|[SecureConnectionLevel](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-secureconnectionlevel.md)|Devuelve el nivel de conexión segura especificado en el archivo RSReportServer.config.|  
|[SenderEmailAddress](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-senderemailaddress.md)|Obtiene la dirección utilizada para enviar el correo electrónico desde el servidor de informes. Solo lectura.|  
|[SendUsingSMTPServer](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-sendusingsmtpserver.md)|Especifica si la propiedad SendUsing en la configuración del correo electrónico está establecida en TRUE.|  
|[SMTPServer](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-smtpserver.md)|Obtiene la propiedad de servidor SMTP a partir del archivo RSReportServer.config. Solo lectura.|  
|[UnattendedExecutionAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-unattendedexecutionaccount.md)|Especifica la cuenta de usuario de inicio de sesión que el servidor de informes suplanta al ejecutarse los informes de forma desatendida. Solo lectura.|  
|[Versión](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-version.md)|Devuelve la versión del servidor de informes.|  
|[Propiedad VirtualDirectoryReportManager &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-virtualdirectoryreportmanager.md)|Devuelve el directorio virtual para la aplicación de administrador de informes.|  
|[Propiedad VirtualDirectoryReportServer &#40;MSReportServer_ConfigurationSetting de WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-virtualdirectoryreportserver.md)|Devuelve el directorio virtual para la aplicación de servicio web del servidor de informes.|  
|[WindowsServiceIdentityActual](../../reporting-services/wmi-provider-library-reference/configurationsetting-property-windowsserviceidentityactual.md)|Devuelve la identidad en la que se ejecuta en la actualidad el servicio de Windows de servidor de informes. Solo lectura.|  
|[WindowsServiceIdentityConfigured](../../reporting-services/wmi-provider-library-reference/windowsserviceidentityconfigured-property.md)|Devuelve la última identidad en la que se configuró el servicio Servidor de informes de Windows para ejecutarse. Solo lectura.|  
  
## <a name="see-also"></a>Consulte también  
 [Miembros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  

  
