---
title: "Métodos MSReportServer_ConfigurationSetting | Documentos de Microsoft"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- MSReportServer_ConfigurationSetting Methods
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- WMI provider [Reporting Services], MSReportServer_ConfigurationSetting class
- MSReportServer_ConfigurationSetting class
ms.assetid: a08c2476-5b8e-4792-94da-1360fe231c6e
caps.latest.revision: 45
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a1206fa05237cd3127db08acc59d69fb0e455261
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="msreportserverconfigurationsetting-methods"></a>Métodos MSReportServer_ConfigurationSetting
  La clase MSReportServer_ConfigurationSetting del proveedor de WMI del servidor de informes proporciona los siguientes métodos públicos.  
  
## <a name="public-methods"></a>Métodos públicos  
  
|||  
|-|-|  
|[BackupEncryptionKey](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-backupencryptionkey.md)|Realiza una copia de seguridad de la clave de cifrado de la instancia. La clave de cifrado se almacena cifrada con una contraseña.|  
|[Método CreateSSLCertificateBinding &#40;MSReportServer_ConfigurationSetting de WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-createsslcertificatebinding.md)|Crea un enlace de certificado SSL.|  
|[DeleteEncryptedInformation](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-deleteencryptedinformation.md)|Elimina la información cifrada de la base de datos del servidor de informes.|  
|[DeleteEncryptionKey](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-deleteencryptionkey.md)|Elimina las claves de cifrado de la base de datos del servidor de informes.|  
|[GenerateDatabaseCreationScript](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabasecreationscript.md)|Genera un script SQL que se puede utilizar para crear la base de datos del servidor de informes.|  
|[GenerateDatabaseRightsScript](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabaserightsscript.md)|Genera un script SQL que se puede utilizar para conceder permisos de usuario a la base de datos del servidor de informes.|  
|[GenerateDatabaseUpgradeScript](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-generatedatabaseupgradescript.md)|Genera un script SQL que se puede utilizar para actualizar una base de datos del servidor de informes.|  
|[Método GetAdminSiteUrl &#40;WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-getadminsiteurl.md)|Obtiene la dirección URL absoluta al sitio web de administración central.|  
|[GetDatabaseVersionDisplayName](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-getdatabaseversiondisplayname.md)|Obtiene el nombre para mostrar para una cadena de versión de base de datos del servidor de informes determinada.|  
|[InitializeReportServer](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-initializereportserver.md)|Inicializa la instancia del servidor de informes especificada.|  
|[Método ListInstalledSharePointVersions &#40;WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listinstalledsharepointversions.md)|Devuelve un conjunto de tokens que representan las versiones de Microsoft [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]o [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] que se instalan en el mismo equipo que el servidor de informes.|  
|[Método ListIPAddresses &#40;MSReportServer_ConfigurationSetting de WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listipaddresses.md)|Enumera las direcciones IP del equipo.|  
|[ListReportServersInDatabase](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listreportserversindatabase.md)|Devuelve una lista de las instalaciones del servidor de informes que se encuentran en la base de datos del servidor de informes, sin tener en cuenta si esas instalaciones tienen acceso a la información segura.|  
|[Método ListReservedURLs &#40;MSReportServer_ConfigurationSetting de WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listreservedurls.md)|Enumera las direcciones URL reservadas para todas las aplicaciones en el servidor de informes.|  
|[Método ListSSLCertificateBindings &#40;MSReportServer_ConfigurationSetting de WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listsslcertificatebindings.md)|Enumera los enlaces de certificados SSL que existen en HTTP.SYS y los esperados desde RSReportServer.config.|  
|[Método ListSSLCertificates &#40;MSReportServer_ConfigurationSetting de WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-listsslcertificates.md)|Enumera los certificados SSL instalados en el equipo.|  
|[ReencryptSecureInformation](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-reencryptsecureinformation.md)|Genera una nueva clave de cifrado y vuelve a cifrar toda la información segura en la base de datos del servidor de informes utilizando esta nueva clave.|  
|[Método RemoveSSLCertificateBindings &#40;MSReportServer_ConfigurationSetting de WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-removesslcertificatebinding.md)|Quita un enlace de certificado SSL.|  
|[RemoveUnattendedExecutionAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-removeunattendedexecutionaccount.md)|Elimina la entrada de cuenta de ejecución desatendida de la configuración del servidor de informes.|  
|[Método RemoveURL &#40;MSReportServer_ConfigurationSetting de WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-removeurl.md)|Quita una dirección URL reservada para el servidor de informes.|  
|[Método ReserveURL &#40;MSReportServer_ConfigurationSetting de WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-reserveurl.md)|Agrega una reserva URL para una aplicación determinada.|  
|[RestoreEncryptionKey](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-restoreencryptionkey.md)|Vuelve a aplicar la clave de cifrado especificada a la base de datos del servidor de informes.|  
|[SetDatabaseConnection](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setdatabaseconnection.md)|Define la conexión de la base de datos del servidor de informes a una base de datos de servidor de informes concreta.|  
|[SetDatabaseLogonTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setdatabaselogontimeout.md)|Especifica el valor de tiempo de espera predeterminado para los intentos de inicio de sesión de la base de datos del servidor de informes.|  
|[SetDatabaseQueryTimeout](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setdatabasequerytimeout.md)|Especifica el valor de tiempo de espera predeterminado para las consultas de la base de datos del servidor de informes.|  
|[SetEmailConfiguration](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setemailconfiguration.md)|Configura la extensión de entrega de correo electrónico utilizada por el servidor de informes para enviar el correo electrónico.|  
|[SetSecureConnectionLevel](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setsecureconnectionlevel.md)|Establece el nivel de conexión segura del servidor de informes.|  
|[SetServiceState](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setservicestate.md)|Activa y desactiva el servicio del servidor de informes.|  
|[SetUnattendedExecutionAccount](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setunattendedexecutionaccount.md)|Especifica la cuenta utilizada para ejecutar informes de forma desatendida.|  
|[Método SetVirtualDirectory &#40;MSReportServer_ConfigurationSetting de WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setvirtualdirectory.md)|Establece el directorio virtual para una aplicación.|  
|[SetWindowsServiceIdentity](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setwindowsserviceidentity.md)|Hace que el servicio del servidor de informes se ejecute como el usuario de Windows especificado y concede a esta cuenta suficientes permisos de sistema de archivos para que el servidor de informes pueda funcionar.|  
  
## <a name="see-also"></a>Vea también  
 [MSReportServer_ConfigurationSetting Class](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
  
