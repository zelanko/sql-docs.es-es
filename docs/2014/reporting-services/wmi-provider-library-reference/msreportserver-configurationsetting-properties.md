---
title: Propiedades MSReportServer_ConfigurationSetting | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- MSReportServer_ConfigurationSetting Properties
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- WMI provider [Reporting Services], MSReportServer_ConfigurationSetting class
- MSReportServer_ConfigurationSetting class
ms.assetid: e75fe1e5-197b-4c65-859b-370821cad003
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: dfaf4fc00a203a67c62b68e1786ed3c53a3f26ba
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59967541"
---
# <a name="msreportserverconfigurationsetting-properties"></a>Propiedades MSReportServer_ConfigurationSetting
  La clase MSReportServer_ConfigurationSetting representa los parámetros de instalación y tiempo de ejecución de una instancia del servidor de informes. La configuración se guarda en el archivo de configuración RSReportServer.config.  
  
## <a name="public-properties"></a>Propiedades públicas  
  
|||  
|-|-|  
|[ConnectionPoolSize](configurationsetting-property-connectionpoolsize.md)|Devuelve el tamaño de grupo de conexiones usado por el servidor de informes para comunicarse con la instancia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] que hospeda la base de datos del servidor de informes. Solo lectura.|  
|[DatabaseLogonAccount](configurationsetting-property-databaselogonaccount.md)|Especifica la cuenta de inicio de sesión usada por el servidor de informes para conectarse a la instancia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] que hospeda la base de datos del servidor de informes. Solo lectura.|  
|[DatabaseLogonTimeout](configurationsetting-property-databaselogontimeout.md)|Especifica el número de segundos de espera antes de que se produzca un error al intentar iniciar sesión en la base de datos del servidor de informes. Solo lectura.|  
|[DatabaseLogonType](configurationsetting-property-databaselogontype.md)|Especifica si el servidor de informes utiliza una cuenta del servicio de Windows, una cuenta de usuario de Windows o un inicio de sesión [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para tener acceso a la base de datos del servidor de informes. Solo lectura.|  
|[DatabaseName](configurationsetting-property-databasename.md)|Especifica el nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda las bases de datos del servidor de informes.|  
|[DatabaseQueryTimeout](configurationsetting-property-databasequerytimeout.md)|Especifica el número de segundos que deben transcurrir antes de que se agote el tiempo de espera del comando o se produzca un error. El servidor de informes está sincronizando el proceso con respecto al catálogo del servidor SQL, no un origen de datos para el informe.|  
|[DatabaseServerName](configurationsetting-property-databaseservername.md)|Especifica el nombre del servidor en el que está instalada la base de datos del servidor de informes.|  
|[Propiedad InstallationID](configurationsetting-property-installationid.md)|Devuelve un identificador único para una instancia del servidor de informes concreta.|  
|[InstanceName](configurationsetting-property-instancename.md)|Especifica el nombre de una instancia del servidor de informes en un equipo específico.|  
|[IsInitialized](configurationsetting-property-isinitialized.md)|Indica si se ha inicializado la instancia del servidor de informes.  Solo lectura.|  
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
  
## <a name="see-also"></a>Vea también  
 [Miembros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
