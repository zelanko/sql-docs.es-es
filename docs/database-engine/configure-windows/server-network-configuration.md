---
title: Configuración de red del servidor | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: configure-windows
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Named Pipes [SQL Server], configuring
- connections [SQL Server], server network configuration
- Database Engine [SQL Server], network configurations
- server network configuration [SQL Server]
- protocols [SQL Server], choosing
- ports [SQL Server], changing
- server configuration [SQL Server]
ms.assetid: 890c09a1-6dad-4931-aceb-901c02ae34c5
caps.latest.revision: 50
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 72b4b52a2977bf5770c9e8a11e5e27fc32ab0396
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="server-network-configuration"></a>Configuración de red del servidor
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Entre las tareas de configuración de red del servidor se incluyen las siguientes: habilitar protocolos, modificar el puerto o canalización usados por un protocolo, configurar el cifrado, configurar el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser, mostrar u ocultar [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] en la red y registrar el nombre de la entidad de seguridad del servidor. La mayoría de las veces, no es necesario cambiar la configuración de red del servidor. Solo debe volver a configurar los protocolos de red del servidor si la red tiene requisitos especiales.  
  
 La configuración de red de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se realiza mediante el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], utilice la Herramienta de red de servidor que se incluye con dichos productos.  
  
## <a name="protocols"></a>Protocolos  
 Utilice el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para habilitar o deshabilitar los protocolos utilizados por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y configurar las opciones disponibles para los protocolos. Se puede habilitar más de un protocolo. Debe habilitar todos los protocolos que desea que utilicen los clientes. Todos los protocolos tienen el mismo acceso al servidor. Para información sobre los protocolos que debe usar, vea [Habilitar o deshabilitar un protocolo de red de servidor](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md) y [Default SQL Server Network Protocol Configuration](../../database-engine/configure-windows/default-sql-server-network-protocol-configuration.md)(Configuración de protocolo de red predeterminada de SQL Server).  
  
### <a name="changing-a-port"></a>Cambiar un puerto  
 Puede configurar los protocolos TCP/IP para que escuchen en un puerto designado. De manera predeterminada, la instancia predeterminada de [!INCLUDE[ssDE](../../includes/ssde-md.md)] escucha en el puerto TCP 1433. Las instancias con nombre de [!INCLUDE[ssDE](../../includes/ssde-md.md)] y [!INCLUDE[ssEW](../../includes/ssew-md.md)] están configuradas para puertos dinámicos. Esto significa que seleccionan un puerto disponible cuando se inicia el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El servicio Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ayuda a los clientes a identificar el puerto cuando se conectan.  
  
 Si se utiliza la configuración para puertos dinámicos, el puerto usado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede cambiar cada vez que se inicia. Si se conecta a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a través de un firewall, debe abrir el puerto usado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Configure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que utilice un puerto específico, así podrá configurar el firewall para que permita la comunicación con el servidor. Para obtener más información, vea [Configurar un servidor para que escuche en un puerto TCP específico &#40;Administrador de configuración de SQL Server&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md).  
  
### <a name="changing-a-named-pipe"></a>Cambiar una canalización con nombre  
 Puede configurar el protocolo de canalizaciones con nombre para que escuche en una canalización con nombre designada. La instancia predeterminada del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] escucha de forma predeterminada en la canalización \\\\.\pipe\sql\query en la instancia predeterminada y en \\\\.\pipe\MSSQL$*\<nombreDeInstancia>* \sql\query en una instancia con nombre. El [!INCLUDE[ssDE](../../includes/ssde-md.md)] solo puede escuchar en una canalización con nombre, pero puede cambiar la canalización a otro nombre si lo desea. El servicio Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ayuda a los clientes a identificar la canalización cuando se conectan. Para obtener más información, vea [Configurar un servidor para escuchar en una canalización alternativa &#40;Administrador de configuración de SQL Server&#41;](../../database-engine/configure-windows/configure-a-server-to-listen-on-an-alternate-pipe.md).  
  
## <a name="force-encryption"></a>Forzar el cifrado  
 El [!INCLUDE[ssDE](../../includes/ssde-md.md)] se puede configurar para requerir el cifrado al comunicarse con aplicaciones cliente. Para obtener más información, vea [Habilitar conexiones cifradas en el motor de base de datos &#40;Administrador de configuración de SQL Server&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md).  
  
## <a name="extended-protection-for-authentication"></a>Protección ampliada para la autenticación  
 La compatibilidad con Protección ampliada para la autenticación mediante el uso del enlace de canal y el enlace de servicio está disponible en los sistemas operativos que admiten Protección ampliada. Para obtener más información, vea [Conectar al motor de base de datos con protección ampliada](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md).  
  
## <a name="authenticating-by-using-kerberos"></a>Autenticar mediante Kerberos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite la autenticación Kerberos. Para obtener más información, vea [Registrar un nombre de entidad de seguridad de servicio para las conexiones con Kerberos](../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md) y [Microsoft Kerberos Configuration Manager para SQL Server](http://www.microsoft.com/download/details.aspx?id=39046).  
  
### <a name="registering-a-server-principal-name-spn"></a>Registrar un nombre de la entidad de seguridad del servidor (SPN)  
 El servicio de autenticación de Kerberos usa un SPN para autenticar un servicio. Para obtener más información, vea [Registrar un nombre de entidad de seguridad de servicio para las conexiones con Kerberos](../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md).  
  
 Los SPN también se pueden utilizar para hacer que la autenticación del cliente sea más segura al conectar con NTLM. Para obtener más información, vea [Conectar al motor de base de datos con protección ampliada](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md).  
  
## <a name="sql-server-browser-service"></a>servicio SQL Server Browser  
 El servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser se ejecuta en el servidor y ayuda a los equipos cliente a encontrar instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No es necesario configurar el servicio Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], pero se debe ejecutar según ciertos escenarios de conexión. Para obtener más información sobre cómo usar el Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Servicio SQL Server Browser &#40;motor de base de datos y SSAS&#41;](../../database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas.md).  
  
## <a name="hiding-sql-server"></a>Ocultar SQL Server  
 Al ejecutarse, el Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] responde a consultas, con la información de nombre, versión y conexión por cada instancia instalada. Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la marca **HideInstance** especifica que el Explorador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no debería responder con información acerca de esta instancia del servidor. Las aplicaciones cliente todavía se pueden conectar, pero deben conocer la información de conexión necesaria. Para obtener más información, vea [Ocultar una instancia del motor de base de datos de SQL Server](../../database-engine/configure-windows/hide-an-instance-of-sql-server-database-engine.md).  
  
## <a name="related-content"></a>Contenido relacionado  
 [Configuración de red de cliente](../../database-engine/configure-windows/client-network-configuration.md)  
  
 [Administrar el servicio del motor de base de datos](../../database-engine/configure-windows/manage-the-database-engine-services.md)  
  
  
