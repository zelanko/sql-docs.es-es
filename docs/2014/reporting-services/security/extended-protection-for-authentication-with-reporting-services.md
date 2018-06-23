---
title: Protección ampliada para la autenticación con Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: eb5c6f4a-3ed5-430b-a712-d5ed4b6b9b2b
caps.latest.revision: 15
author: markingmyname
ms.author: maghan
manager: mblythe
ms.openlocfilehash: b19170e93dbf4efb973df44fc9788c9659897424
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103973"
---
# <a name="extended-protection-for-authentication-with-reporting-services"></a>Protección ampliada para la autenticación con Reporting Services
  En versiones recientes del sistema operativo [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, la protección ampliada es un conjunto de mejoras. La protección ampliada mejora cómo protegen las aplicaciones las credenciales y la autenticación. La propia característica no proporciona directamente protección contra ataques específicos como el reenvío de credenciales, pero proporciona una infraestructura para aplicaciones como [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] para aplicar la protección ampliada para la autenticación.  
  
 Las principales mejoras de autenticación que forman parte de la protección ampliada son los enlaces de servicio y de canal. El enlace de canal usa un token de enlace de canal (CBT) para comprobar que no se ha puesto en peligro el canal establecido entre dos extremos. El enlace de servicio usa nombres principales de servicio (SPN) para validar el destino previsto de los tokens de autenticación. Para obtener información general sobre la protección ampliada, vea [Autenticación de Windows integrada con protección ampliada](http://go.microsoft.com/fwlink/?LinkId=179922).  
  
 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] admite y aplica la protección ampliada que se ha habilitado en el sistema operativo y configurado en [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. De forma predeterminada, [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] acepta solicitudes que especifican la autenticación Negotiate o NTLM y, por tanto, pueden beneficiarse de la compatibilidad de la protección ampliada del sistema operativo y de las características de la protección ampliada de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  De forma predeterminada, Windows no habilita la protección ampliada. Para obtener información sobre cómo habilitar la protección ampliada de Windows, vea [Protección ampliada para la autenticación](http://go.microsoft.com/fwlink/?LinkID=178431). Tanto el sistema operativo como la pila de autenticación de cliente deben ser compatibles con la protección ampliada para la autenticación se realice correctamente. En sistemas operativos más antiguos, quizá deba instalar varias actualizaciones para disponer de un equipo totalmente preparado para la protección ampliada. Para obtener información sobre los desarrollos recientes con la protección ampliada, vea [Actualizar información con protección ampliada](http://go.microsoft.com/fwlink/?LinkId=183362).  
  
## <a name="reporting-services-extended-protection-overview"></a>Información general sobre la protección ampliada de Reporting Services  
 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] admite y aplica la protección extendida que se ha habilitado en el sistema operativo. Si el sistema operativo no admite la protección ampliada o no se ha habilitado la característica en él, se producirá un error de autenticación de la característica de protección ampliada de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] . [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] La protección ampliada también requiere un certificado SSL. Para más información, vea [Configurar conexiones SSL en un servidor de informes en modo nativo](configure-ssl-connections-on-a-native-mode-report-server.md).  
  
> [!IMPORTANT]  
>  De forma predeterminada, [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] no se habilita la protección ampliada. La característica se puede habilitar si se modifica el archivo de configuración `rsreportserver.config` o mediante las API de WMI para actualizar el archivo de configuración. [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)][!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] no proporciona una interfaz de usuario para modificar o ver la configuración de protección ampliada. Para obtener más información, vea la sección de [configuración](#ConfigurationSettings) de este tema.  
  
 Los problemas comunes que se producen a causa de los cambios de la configuración de la protección ampliada o de una configuración incorrecta no se muestran mediante mensajes ni ventanas de cuadro de diálogo de error obvios. Los problemas relacionados con la configuración y la compatibilidad de la protección ampliada tienen como resultado errores de autenticación y errores en los registros de seguimiento de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Algunas tecnologías de acceso a datos pueden no admitir la protección ampliada. Para conectar los orígenes de datos de SQL Server y la base de datos del catálogo [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] se usa una tecnología de acceso a datos. El hecho de que una tecnología de acceso a datos no admite la protección ampliada afecta a [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] de las maneras siguientes:  
>   
>  -   El servidor SQL Server que ejecuta la base de datos del catálogo [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] no puede tener habilitada la protección ampliada; de lo contrario se producirá un error de conexión entre el servidor de informes y la base de datos del catálogo, y se devolverán errores de autenticación.  
> -   Servidores SQL Server que se usan como [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] informe orígenes de datos no pueden tener habilitada la protección ampliada o los intentos realizados por el servidor de informes para conectarse al origen de datos del informe provocarán errores y devolverán errores de autenticación.  
>   
>  La documentación de una tecnología de acceso a datos debe tener información sobre la compatibilidad con la protección ampliada.  
  
### <a name="upgrade"></a>UPGRADE  
  
-   Actualizar una [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] servidor [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] agrega valores de configuración con valores predeterminados para el `rsreportserver.config` archivo. Si ya estuviera presente, la configuración de la [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] instalación conservará en el `rsreportserver.config` archivo.  
  
-   Cuando se agregan los valores de configuración a la `rsreportserver.config` archivo de configuración, el comportamiento predeterminado es el [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] característica de protección ampliada desactivado y debe habilitar la característica como se describe en este tema. Para obtener más información, vea la sección de [configuración](#ConfigurationSettings) de este tema.  
  
-   El valor predeterminado del parámetro `RSWindowsExtendedProtectionLevel` es `Off`.  
  
-   El valor predeterminado del parámetro `RSWindowsExtendedProtectionScenario` es `Proxy`.  
  
-   [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] El Asesor de actualizaciones no comprueba que el sistema operativo o la instalación actual de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] tiene habilitada la compatibilidad con protección ampliada.  
  
### <a name="what-reporting-services-extended-protection-does-not-cover"></a>Lo que no cubre la protección ampliada de Reporting Services  
 Las siguientes áreas de características y escenarios no son compatibles con el [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] característica de protección ampliada:  
  
-   Los autores de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] extensiones de seguridad personalizadas deben agregar compatibilidad para la protección ampliada a su extensión de seguridad personalizado.  
  
-   Componentes de terceros agregados o usados por un [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] instalación debe actualizarse por el proveedor de terceros, para admitir la protección extendida. Para obtener más información, póngase en contacto con el otro proveedor.  
  
## <a name="deployment-scenarios-and-recommendations"></a>Escenarios y recomendaciones para la implementación  
 En los siguientes escenarios se ilustran las distintas implementaciones y topologías, así como la configuración recomendada para protegerlas con la protección ampliada de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
### <a name="direct"></a>Directo  
 Este escenario describe la conexión directa con un servidor de informes, por ejemplo, el entorno de una intranet.  
  
|Escenario|Diagrama del escenario|Protección|  
|--------------|----------------------|-------------------|  
|Comunicación de SSL directa.<br /><br /> El servidor de informes aplicará el cliente en el enlace de canal del servidor de informes.|![RS_ExtendedProtection_DirectSSL](../media/rs-extendedprotection-directssl.gif "RS_ExtendedProtection_DirectSSL")<br /><br /> 1) Aplicación cliente<br /><br /> 2) Servidor de informes|El enlace de servicio no es necesario porque el enlace de canal usará el canal SSL.<br /><br /> Establecer `RSWindowsExtendedProtectionLevel` a `Allow` o `Require`.<br /><br /> Establecer `RSWindowsExtendedProtectionScenario` a `Direct`.|  
|Comunicación HTTP directa. El servidor de informes aplicará el cliente en el enlace de servicio del servidor de informes.|![RS_ExtendedProtection_Direct](../media/rs-extendedprotection-direct.gif "RS_ExtendedProtection_Direct")<br /><br /> 1) Aplicación cliente<br /><br /> 2) Servidor de informes|No existe ningún canal SSL y, por tanto, no es posible la aplicación del enlace de canal.<br /><br /> El enlace de servicio se puede validar. Sin embargo, no es una defensa completa sin el enlace de canal y el enlace de servicio por sí mismo solo protegerá contra amenazas básicas.<br /><br /> Establecer `RSWindowsExtendedProtectionLevel` a `Allow` o `Require`.<br /><br /> Establecer `RSWindowsExtendedProtectionScenario` a `Any`.|  
  
### <a name="proxy-and-network-load-balancing"></a>Equilibrio de carga del proxy y de la red  
 Las aplicaciones cliente se conectan a un dispositivo o software que realiza SSL y pasa por las credenciales al servidor para la autenticación, por ejemplo, una extranet, Internet o una intranet segura. El cliente se conecta a un proxy o todos los clientes usan un proxy.  
  
 Ocurre lo mismo cuando usa un dispositivo de equilibrio de carga de red (NLB).  
  
|Escenario|Diagrama del escenario|Protección|  
|--------------|----------------------|-------------------|  
|Comunicación HTTP. El servidor de informes aplicará el cliente en el enlace de servicio del servidor de informes.|![RS_ExtendedProtection_Indirect](../media/rs-extendedprotection-indirect.gif "RS_ExtendedProtection_Indirect")<br /><br /> 1) Aplicación cliente<br /><br /> 2) Servidor de informes<br /><br /> 3) Proxy|No existe ningún canal SSL y, por tanto, no es posible la aplicación del enlace de canal.<br /><br /> Establecer `RSWindowsExtendedProtectionLevel` a `Allow` o `Require`.<br /><br /> Establecer `RSWindowsExtendedProtectionScenario` a `Any`.<br /><br /> Tenga en cuenta que el servidor de informes debe configurarse para saber el nombre del servidor proxy para asegurarse de que el enlace de servicio se aplica correctamente.|  
|Comunicación HTTP.<br /><br /> El servidor de informes aplicará el cliente en el enlace de canal de proxy y en el enlace de servicio del servidor de informes.|![RS_ExtendedProtection_Indirect_SSL](../media/rs-extendedprotection-indirect-ssl.gif "RS_ExtendedProtection_Indirect_SSL")<br /><br /> 1) Aplicación cliente<br /><br /> 2) Servidor de informes<br /><br /> 3) Proxy|El canal SSL al proxy está disponible. Por tanto, se puede aplicar el enlace de canal en el proxy.<br /><br /> También se puede aplicar el enlace de servicio.<br /><br /> El servidor de informes debe saber el nombre del proxy y el administrador del servidor de informes debe crear una reserva de direcciones URL para este, con un encabezado de host o configurar el nombre de proxy en la entrada del Registro de Windows `BackConnectionHostNames`.<br /><br /> `RSWindowsExtendedProtectionLevel` para `Allow` o `Require`.<br /><br /> Establecer `RSWindowsExtendedProtectionScenario` a `Proxy`.|  
|Comunicación HTTPS indirecta con un proxy seguro. El servidor de informes aplicará el cliente en el enlace de canal de proxy y en el enlace de servicio del servidor de informes.|![RS_ExtendedProtection_IndirectSSLandHTTPS](../media/rs-extendedprotection-indirectsslandhttps.gif "RS_ExtendedProtection_IndirectSSLandHTTPS")<br /><br /> 1) Aplicación cliente<br /><br /> 2) Servidor de informes<br /><br /> 3) Proxy|El canal SSL al proxy está disponible. Por tanto, se puede aplicar el enlace de canal en el proxy.<br /><br /> También se puede aplicar el enlace de servicio.<br /><br /> El servidor de informes debe saber el nombre del proxy y el administrador del servidor de informes debe crear una reserva de direcciones URL para este, con un encabezado de host o configurar el nombre de proxy en la entrada del Registro de Windows `BackConnectionHostNames`.<br /><br /> `RSWindowsExtendedProtectionLevel` para `Allow` o `Require`.<br /><br /> Establecer `RSWindowsExtendedProtectionScenario` a `Proxy`.|  
  
### <a name="gateway"></a>Puerta de enlace  
 En este escenario se describen las aplicaciones cliente que se conectan a un dispositivo o software que realiza SSL y autentica al usuario. Después, el dispositivo o software suplanta el contexto del usuario o un contexto de usuario distinto antes de efectuar una solicitud al servidor de informes.  
  
|Escenario|Diagrama del escenario|Protección|  
|--------------|----------------------|-------------------|  
|Comunicación HTTP indirecta.<br /><br /> La puerta de enlace aplicará el cliente en un enlace de canal de puerta de enlace. Existe una puerta de enlace en el enlace de servicio del servidor de informes.|![RS_ExtendedProtection_Indirect_SSL](../media/rs-extendedprotection-indirect-ssl.gif "RS_ExtendedProtection_Indirect_SSL")<br /><br /> 1) Aplicación cliente<br /><br /> 2) Servidor de informes<br /><br /> 3) Dispositivo de puerta de enlace|El enlace de canal desde el cliente al servidor de informes no es posible ya que la puerta de enlace suplanta un contexto y, por tanto, crea un nuevo token NTLM.<br /><br /> No existe ningún SSL desde la puerta de enlace al servidor de informes, por tanto, no se puede aplicar ningún enlace de canal.<br /><br /> Se puede aplicar el enlace de servicio.<br /><br /> Establecer `RSWindowsExtendedProtectionLevel` a `Allow` o `Require`.<br /><br /> Establecer `RSWindowsExtendedProtectionScenario` a `Any`.<br /><br /> El dispositivo de puerta de enlace lo debe configurar el administrador para aplicar el enlace de canal.|  
|Comunicación HTTPS indirecta con una puerta de enlace segura. La puerta de enlace aplicará el cliente en el enlace de canal de puerta de entrada y el servidor de informes aplicará la puerta de enlace en el enlace de canal del servidor de informes.|![RS_ExtendedProtection_IndirectSSLandHTTPS](../media/rs-extendedprotection-indirectsslandhttps.gif "RS_ExtendedProtection_IndirectSSLandHTTPS")<br /><br /> 1) Aplicación cliente<br /><br /> 2) Servidor de informes<br /><br /> 3) Dispositivo de puerta de enlace|El enlace de canal desde el cliente al servidor de informes no es posible ya que la puerta de enlace suplanta un contexto y, por tanto, crea un nuevo token NTLM.<br /><br /> SSL desde la puerta de enlace al servidor de informes, es decir, se puede aplicar enlace de canal.<br /><br /> No se requiere enlace de servicio.<br /><br /> Establecer `RSWindowsExtendedProtectionLevel` a `Allow` o `Require`.<br /><br /> Establecer `RSWindowsExtendedProtectionScenario` a `Direct`.<br /><br /> El dispositivo de puerta de enlace lo debe configurar el administrador para aplicar el enlace de canal.|  
  
### <a name="combination"></a>Combinación  
 Este escenario describe los entornos de extranet o Internet en los que el cliente se conecta con un proxy. Se combina con un entorno de intranet donde un cliente se conecta con un servidor de informes.  
  
|Escenario|Diagrama del escenario|Protección|  
|--------------|----------------------|-------------------|  
|Acceso indirecto y directo desde el cliente al servicio del servidor de informes sin SSL en conexiones del cliente al proxy ni del cliente al servidor de informes.|1) Aplicación cliente<br /><br /> 2) Servidor de informes<br /><br /> 3) Proxy<br /><br /> 4) Aplicación cliente|Se puede aplicar el enlace de servicio desde el cliente al servidor de informes.<br /><br /> El servidor de informes debe saber el nombre del proxy y el administrador del servidor de informes debe crear una reserva de direcciones URL para este, con un encabezado de host o configurar el nombre de proxy en la entrada del Registro de Windows `BackConnectionHostNames`.<br /><br /> Establecer `RSWindowsExtendedProtectionLevel` a `Allow` o `Require`.<br /><br /> Establecer `RSWindowsExtendedProtectionScenario` a `Any`.|  
|Acceso indirecto y directo desde el cliente al servidor de informes donde el cliente establece una conexión SSL al proxy o al servidor de informes.|![RS_ExtendedProtection_CombinationSSL](../media/rs-extendedprotection-combinationssl.gif "RS_ExtendedProtection_CombinationSSL")<br /><br /> 1) Aplicación cliente<br /><br /> 2) Servidor de informes<br /><br /> 3) Proxy<br /><br /> 4) Aplicación cliente|Se puede usar el enlace de canal<br /><br /> El servidor de informes debe saber el nombre del proxy y el administrador del servidor de informes debe crear una reserva de direcciones URL para el proxy, con un encabezado de host o configurar el nombre de proxy en la entrada del Registro de Windows `BackConnectionHostNames`.<br /><br /> Establecer `RSWindowsExtendedProtectionLevel` a `Allow` o `Require`.<br /><br /> Establecer `RSWindowsExtendedProtectionScenario` a `Proxy`.|  
  
## <a name="configuring-reporting-rervices-extended-protection"></a>Configurar la protección ampliada de Reporting Services  
 El `rsreportserver.config` archivo contiene los valores de configuración que controlan el comportamiento de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] protección ampliada.  
  
 Para obtener más información acerca del uso y editar la `rsreportserver.config` de archivos, consulte [archivo de configuración RSReportServer](../report-server/rsreportserver-config-configuration-file.md). La configuración de la protección ampliada también se puede cambiar e inspeccionar mediante las API WMI. Para obtener más información, consulte [método SetExtendedProtectionSettings &#40;MSReportServer_ConfigurationSetting de WMI&#41;](../wmi-provider-library-reference/configurationsetting-method-setextendedprotectionsettings.md).  
  
 Cuando se produce un error de autenticación de la configuración, se deshabilitan los tipos de autenticación `RSWindowsNTLM`, `RSWindowsKerberos` y `RSWindowsNegotiate` en el servidor de informes.  
  
###  <a name="ConfigurationSettings"></a> Configuración de la protección ampliada de los servicios de informes  
 En la tabla siguiente proporciona información sobre las opciones de configuración que aparecen en la `rsreportserver.config` para la protección extendida.  
  
|Configuración|Descripción|  
|-------------|-----------------|  
|`RSWindowsExtendedProtectionLevel`|Especifica el grado de aplicación de la protección ampliada. Los valores válidos son `Off`, `Allow`, y `Require`.<br /><br /> El valor predeterminado es `Off`.<br /><br /> El valor `Off` especifica que no existe comprobación de enlace de canal ni de enlace de servicio.<br /><br /> El valor `Allow` admite la protección ampliada pero no la necesita. El valor Allow especifica:<br /><br /> La protección ampliada se aplicará en las aplicaciones cliente que se ejecuten en sistemas operativos que la admitan. La forma de aplicar la protección la determina la opción `RsWindowsExtendedProtectionScenario`.<br /><br /> Se permitirá la autenticación en aplicaciones que se ejecuten en sistemas operativos que no sean compatibles con la protección ampliada.<br /><br /> El valor `Require` especifica:<br /><br /> La protección ampliada se aplicará en las aplicaciones cliente que se ejecuten en sistemas operativos que la admitan.<br /><br /> **No** se permitirá la autenticación en aplicaciones que se ejecuten en sistemas operativos que no sean compatibles con la protección ampliada.|  
|`RsWindowsExtendedProtectionScenario`|Especifica las formas de la protección ampliada que se validan: enlace de canal, enlace de servicio o ambos. Los valores válidos son `Any`, `Proxy`, y `Direct`.<br /><br /> El valor predeterminado es `Proxy`.<br /><br /> El valor `Any` especifica:<br /><br /> -No se necesitan la autenticación de Windows NTLM, Kerberos ni Negotiate, ni ningún enlace de canal.<br /><br /> -Se aplica el enlace de servicio.<br /><br /> El valor `Proxy` especifica:<br /><br /> -Si está presente, la autenticación de Windows NTLM, Kerberos y Negotiate cuando está presente un token de enlace de canal.<br /><br /> -Se aplica el enlace de servicio.<br /><br /> El valor `Direct` especifica:<br /><br /> -La autenticación de Windows NTLM, Kerberos y Negotiate cuando están presentes un CBT y una conexión SSL al servicio actual, y el CBT para que la conexión SSL coincida con el CBT del token de NTLM, Kerberos o Negotiate.<br /><br /> -No se aplica el enlace de servicio.<br /><br /> <br /><br /> Nota: Este valor se omite si `RsWindowsExtendedProtectionLevel` está establecido en `OFF`.|  
  
 Entradas de ejemplo en el `rsreportserver.config` archivo de configuración:  
  
```  
<Authentication>  
         <RSWindowsExtendedProtectionLevel>Allow</RSWindowsExtendedProtectionLevel>  
         <RSWindowsExtendedProtectionScenario>Proxy</RSWindowsExtendedProtectionLevel>  
</Authentication>  
```  
  
## <a name="service-binding-and-included-spns"></a>Enlace de servicio y SPN incluidos  
 El enlace de servicio usa nombres principales de servicio (SPN) para validar el destino previsto de los tokens de autenticación. [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] usa la información de reserva de dirección URL para generar una lista de los SPN que se consideran válidos. Si se usa la información de reservas de direcciones URL para la validación tanto de SPN como de reservas de direcciones URL, los administraciones del sistema pueden administrarlos desde una sola ubicación.  
  
 La lista de los SPN válidos se actualiza cuando se inicia el servidor de informes, se cambia la configuración de la protección ampliada o se recicla el dominio de aplicación.  
  
 La lista válida de los SPN es específica de cada aplicación. Por ejemplo, el Administrador de informes y el servidor de informes tendrán cada uno una lista distinta de los SPN válidos calculados.  
  
 La lista de los SPN válidos calculados para una aplicación la determinan los siguientes factores:  
  
-   Cada reserva de direcciones URL.  
  
-   Cada SPN recuperado desde el controlador de dominios para la cuenta de servicio de los servicios de informes.  
  
-   Si una reserva de direcciones URL incluye caracteres comodín ('*' o '+'), el servidor de informes agregará cada entrada desde la colección de hosts.  
  
### <a name="hosts-collection-sources"></a>Orígenes de la colección de hosts.  
 En la tabla siguiente se citan los posible orígenes para la colección de hosts.  
  
|Tipo de origen de datos|Descripción|  
|--------------------|-----------------|  
|ComputerNameDnsDomain|El nombre del dominio DNS asignado al equipo local. Si el equipo local es un nodo de un clúster, se usa el nombre de dominio DNS del servidor virtual de clústeres.|  
|ComputerNameDnsFullyQualified|El nombre DNS completo que identifica exclusivamente el equipo local. Este nombre es una combinación del nombre del host DNS y el nombre del dominio DNS, con el formato *nombreDeHost*.*nombreDeDominio*. Si el equipo local es un nodo de un clúster, se usa el nombre DNS completo del servidor virtual de clústeres.|  
|ComputerNameDnsHostname|El nombre del host DNS del equipo local. Si el equipo local es un nodo de un clúster, se usa el nombre del host DNS del servidor virtual de clústeres.|  
|ComputerNameNetBIOS|El nombre NetBIOS del equipo local. Si el equipo local es un nodo de un clúster, se usa el nombre NetBIOS del servidor virtual de clústeres.|  
|ComputerNamePhysicalDnsDomain|El nombre del dominio DNS asignado al equipo local. Si el equipo local es un nodo de un clúster, se usa el nombre de dominio DNS del equipo local, no el nombre del servidor virtual de clústeres.|  
|ComputerNamePhysicalDnsFullyQualified|El nombre DNS completo que identifica exclusivamente el equipo. Si el equipo local es un nodo de un clúster, se usa el nombre DNS completo del equipo local, no el nombre del servidor virtual de clústeres.<br /><br /> El nombre DNS completo es una combinación del nombre del host DNS y del nombre del dominio DNS, con el formato *nombreDeHost*.*nombreDeDominio*.|  
|ComputerNamePhysicalDnsHostname|El nombre del host DNS del equipo local. Si el equipo local es un nodo de un clúster, se usa el nombre del host DNS del equipo local, no el nombre del servidor virtual de clústeres.|  
|ComputerNamePhysicalNetBIOS|El nombre NetBIOS del equipo local. Si el equipo local es un nodo de un clúster, se usa el nombre NetBIOS del equipo local, no el nombre del servidor virtual de clústeres.|  
  
 A medida que se agregan los SPN, se agrega una entrada al registro de seguimiento con la siguiente apariencia:  
  
 `rshost!rshost!10a8!01/07/2010-19:29:38:: i INFO: SPN Whitelist Added <ComputerNamePhysicalNetBIOS> - <theservername>.`  
  
 `rshost!rshost!10a8!01/07/2010-19:29:38:: i INFO: SPN Whitelist Added <ComputerNamePhysicalDnsHostname> - <theservername>.`  
  
 Para más información, vea [Registrar un nombre principal de servicio &#40;SPN&#41; para un servidor de informes](../report-server/register-a-service-principal-name-spn-for-a-report-server.md) y [Acerca de las reservas y el registro de reservas de URL &#40;Administrador de configuración de SSRS&#41;](../install-windows/about-url-reservations-and-registration-ssrs-configuration-manager.md).  
  
## <a name="see-also"></a>Vea también  
 [Conectar al motor de base de datos con protección ampliada](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md)   
 [Introducción a la protección ampliada para la autenticación](http://go.microsoft.com/fwlink/?LinkID=177943)   
 [Autenticación de Windows integrada con protección ampliada](http://go.microsoft.com/fwlink/?LinkId=179922)   
 [Asesor de seguridad de Microsoft: protección ampliada para la autenticación](http://go.microsoft.com/fwlink/?LinkId=179923)   
 [Registro de seguimiento de servicio de servidor de informes](../report-server/report-server-service-trace-log.md)   
 [Archivo de configuración RSReportServer](../report-server/rsreportserver-config-configuration-file.md)   
 [Método SetExtendedProtectionSettings &#40;MSReportServer_ConfigurationSetting de WMI&#41;](../wmi-provider-library-reference/configurationsetting-method-setextendedprotectionsettings.md)  
  
  