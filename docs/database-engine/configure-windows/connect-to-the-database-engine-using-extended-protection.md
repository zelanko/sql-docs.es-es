---
title: "Conectar al motor de base de datos con protección ampliada | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- spoofing attacks
- service binding
- luring attacks
- Schannel
- channel binding
- Extended Protection
ms.assetid: ecfd783e-7dbb-4a6c-b5ab-c6c27d5dd57f
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 894f04fe8bf8df95bb288acab897f3274fbacb18
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="connect-to-the-database-engine-using-extended-protection"></a>Conectar al motor de base de datos con protección ampliada
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite la **protección ampliada** a partir de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]. La**protección ampliada para la autenticación** es una característica de los componentes de red que implementa el sistema operativo. La**protección ampliada** se admite en Windows 7 y Windows Server 2008 R2. **Protección ampliada** se incluye en Service packs para [!INCLUDE[msCoName](../../includes/msconame-md.md)] sistemas operativos antiguos. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es más seguro cuando las conexiones se realizan con **Extended Protection**.  
  
> [!IMPORTANT]  
>  Windows no habilita la **protección ampliada** de forma predeterminada. Para obtener información acerca de cómo habilitar la **protección ampliada** en Windows, vea [Protección ampliada para la autenticación](http://support.microsoft.com/kb/968389).  
  
## <a name="description-of-extended-protection"></a>Descripción de la protección ampliada  
 La**protección ampliada** usa el enlace de servicio y el enlace de canal para ayudar a evitar un ataque de retransmisión de autenticación. En un ataque de retransmisión de autenticación, un cliente que puede realizar la autenticación NTLM (por ejemplo, el Explorador de Windows, [!INCLUDE[msCoName](../../includes/msconame-md.md)] Outlook, una aplicación .NET SqlClient, etc.) se conecta a un atacante (por ejemplo, un servidor de archivos CIFS malintencionado). El atacante utiliza las credenciales del cliente para hacerse pasar por este y autenticarse en un servicio (por ejemplo, una instancia del servicio [!INCLUDE[ssDE](../../includes/ssde-md.md)] ).  
  
 Hay dos variaciones de este ataque:  
  
-   En un ataque por señuelo, el cliente es atraído para conectar voluntariamente con el atacante.  
  
-   En un ataque de suplantación, el cliente pretende conectarse a un servicio válido, pero no es consciente de que DNS o el enrutamiento IP, o ambos, se han alterado para redirigir la conexión al atacante en su lugar.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite el enlace de servicio y el enlace de canal para ayudar a reducir estos ataques en sesiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="service-binding"></a>enlace del servicio  
 El enlace de servicio soluciona los ataques por señuelo exigiendo que un cliente envíe un nombre principal de servicio (SPN) firmado del servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al que el cliente pretende conectarse. Como parte de la respuesta de la autenticación, el servicio valida que el SPN recibido en el paquete coincida con su propio SPN. Si un cliente es atraído para conectarse a un atacante, el cliente incluirá el SPN firmado del atacante. El atacante no puede retransmitir el paquete para autenticar al servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] real como el cliente, porque incluiría el SPN del atacante. El enlace de servicio incurre en un costo insignificante una sola vez, pero no soluciona los ataques de suplantación. El enlace de servicio se produce cuando una aplicación cliente no usa el cifrado para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="channel-binding"></a>enlace del canal  
 El enlace de canal establece un canal seguro (Schannel) entre un cliente y una instancia del servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El servicio comprueba la autenticidad del cliente comparando el token de enlace de canal (CBT) del cliente específico de ese canal, con su propio CBT. El enlace de canal trata tanto los ataques de suplantación como los de atracción. Sin embargo, incurre en un costo de tiempo de ejecución mayor, porque requiere cifrado de Seguridad de la capa de transporte (TLS) de todo el tráfico de la sesión. El enlace de canal se produce cuando una aplicación cliente usa el cifrado para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], independientemente de si el cifrado lo fuerza el cliente o el servidor.  
  
> [!WARNING]  
>  Los proveedores de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[msCoName](../../includes/msconame-md.md)] de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admiten TLS 1.0 y SSL 3.0. Si fuerza un protocolo diferente (como por ejemplo, TLS 1.1 o TLS 1.2) realizando cambios en la capa SChannel del sistema operativo, las conexiones a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podrían no funcionar como es debido.  
  
### <a name="operating-system-support"></a>Sistemas operativos admitidos  
 Los siguientes vínculos proporcionan más información acerca del modo en que Windows admite la **protección ampliada**:  
  
-   [Autenticación de Windows integrada con protección ampliada](http://msdn.microsoft.com/library/dd639324.aspx)  
  
-   [Asesor de seguridad de Microsoft (973811), protección ampliada para la autenticación](http://www.microsoft.com/technet/security/advisory/973811.mspx)  
  
## <a name="settings"></a>Configuración  
 Hay tres opciones de configuración de la conexión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que afectan al enlace de servicio y al enlace de canal. Las opciones se pueden configurar utilizando el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o WMI, y se pueden ver mediante la faceta **Configuración del protocolo del servidor** de la administración basada en directivas.  
  
-   **Forzar el cifrado**  
  
     Los valores posibles son **Activado** y **Desactivado**. Para usar el enlace de canal, **Forzar cifrado** debe estar establecido en **Activado**y todos los clientes se verán obligados a realizar el cifrado. Si es **Desactivado**, solo se garantiza el enlace de servicio. **Forzar cifrado** está en **Propiedades de Protocolos de MSSQLSERVER (pestaña Marcas)** en el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   **Protección ampliada**  
  
     Los valores posibles son **Desactivado**, **Permitido**y **Requerido**. La variable **Protección ampliada** permite a los usuarios configurar el nivel de **protección ampliada** de cada sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . **Protección extendida** está en **Propiedades de Protocolos de MSSQLSERVER (pestaña Avanzadas)** en el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    -   Cuando se establece en **Desactivado**, **Protección ampliada** se deshabilita. La instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aceptará las conexiones de cualquier cliente independientemente de que esté o no protegido. La configuración**Desactivado** es compatible con los sistemas operativos sin revisiones y anteriores, pero es menos segura. Utilice este valor cuando sepa que los sistemas operativos clientes no admiten la protección ampliada.  
  
    -   Cuando se establece en **Permitido**, la **protección ampliada** se requiere para las conexiones de los sistemas operativos que admiten la **protección ampliada**. La**protección ampliada** se omite para las conexiones de los sistemas operativos que no admiten la **protección ampliada**. Se rechazan las conexiones de las aplicaciones cliente no protegidas que se estén ejecutando en sistemas operativos clientes protegidos. Esta configuración es más segura que **Desactivado**, pero no es la más segura. Utilice esta configuración en entornos mixtos, donde no todos los sistemas operativos admitan **protección ampliada** .  
  
    -   Cuando se establece en **Requerido**, solo se aceptan las conexiones de las aplicaciones protegidas en sistemas operativos protegidos. Esta configuración es la más segura, pero los sistemas operativos o las aplicaciones que no admitan la **protección ampliada** no podrán conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   **Se aceptan SPN NTLM**  
  
     Cuando un servidor se conoce por más de un SPN, se necesita la variable **Se aceptan SPN NTLM** . Cuando un cliente intenta conectarse al servidor utilizando un SPN válido que el servidor no conoce, el enlace de servicio dará un error. Para evitar este problema, los usuarios pueden especificar varios SPN que representan al servidor utilizando **Se aceptan SPN NTLM**. **Se aceptan SPN NTLM** es una serie de SPN separados por punto y coma. Por ejemplo, para permitir los SPN **MSSQLSvc/ nombreDeHost1.Contoso.com** y **MSSQLSvc/ nombreDeHost2.Contoso.com**, escriba **MSSQLSvc/nombreDeHost1 .Contoso.com; MSSQLSvc/nombreDeHost2.Contoso.com** en el cuadro **Se aceptan SPN NTLM** . La variable tiene una longitud máxima de 2.048 caracteres. **Se aceptan SPN NTLM** está en **Propiedades de Protocolos de MSSQLSERVER (pestaña Avanzadas)** en el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="enabling-extended-protection-for-the-database-engine"></a>Habilitar la protección ampliada para el motor de base de datos  
 Para usar la **protección ampliada**, tanto el servidor como el cliente deben tener un sistema operativo en el que se admita la **protección ampliada**y la **protección ampliada** debe estar habilitada en el sistema operativo. Para obtener más información acerca de cómo habilitar la **protección ampliada** para el sistema operativo, vea [Protección ampliada para la autenticación](http://support.microsoft.com/kb/968389).  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite la **protección ampliada** a partir de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]. La**protección ampliada** para algunas versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estará disponible en actualizaciones futuras. Después de habilitar la **protección ampliada** en el equipo servidor, siga estos pasos para volver a habilitar la **protección ampliada**en el motor de base de datos:  
  
1.  En el menú **Inicio** , elija **Todos los programas**, elija **Microsoft SQL Server** y haga clic en **Administrador de configuración de SQL Server**.  
  
2.  Expanda **Configuración de red de SQL Server**, haga clic con el botón derecho en **Protocolos de** *\<*nombreDeInstancia*>*y, luego, haga clic en **Propiedades**.  
  
3.  Para el enlace de canal y el enlace de servicio, en la pestaña **Opciones avanzadas** , establezca **Protección ampliada** en el valor adecuado.  
  
4.  Si lo desea, cuando un servidor se conozca por más de un SPN, en la pestaña **Opciones avanzadas** , configure el campo **Se aceptan SPN NTLM** tal y como se describe en la sección "Configuración".  
  
5.  Para el enlace de canal, en la pestaña **Marcas** , establezca **Forzar cifrado** en **Activado**.  
  
6.  Reinicie el servicio [!INCLUDE[ssDE](../../includes/ssde-md.md)] .  
  
## <a name="configuring-other-sql-server-components"></a>Configurar otros componentes de SQL Server  
 Para obtener más información sobre cómo configurar [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vea [Protección ampliada para la autenticación con Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md).  
  
 Al utilizar IIS para tener acceso a los datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utilizando una conexión HTTPS o HTTP, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] pueden sacar provecho de la protección ampliada que proporciona IIS. Para obtener más información acerca de cómo configurar IIS para utilizar la protección ampliada, vea el tema que trata cómo [configurar la protección ampliada en IIS 7.5](http://go.microsoft.com/fwlink/?LinkId=181105).  
  
## <a name="see-also"></a>Vea también  
 [Configuración de red del servidor](../../database-engine/configure-windows/server-network-configuration.md)   
 [Configuración de red de cliente](../../database-engine/configure-windows/client-network-configuration.md)   
 [Introducción a la protección ampliada para la autenticación](http://go.microsoft.com/fwlink/?LinkID=177943)   
 [Autenticación de Windows integrada con protección ampliada](http://go.microsoft.com/fwlink/?LinkId=179922)  
  
  
