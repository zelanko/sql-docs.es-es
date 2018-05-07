---
title: Compatibilidad de nombre Principal de servicio (SPN) en conexiones de cliente | Documentos de Microsoft
description: Compatibilidad de nombre Principal de servicio (SPN) en conexiones de cliente
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|features
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, SPNs
- OLE DB, SPNs
- SPNs [SQL Server]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: c119c14cbd0441d22b8e97f8d168d10d652e86d7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="service-principal-name-spn-support-in-client-connections"></a>Compatibilidad con Nombre de la entidad de seguridad del servicio (SPN) en conexiones cliente
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  A partir de [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], se ha ampliado la compatibilidad con nombres principales de servicio (SPN) para habilitar la autenticación mutua en todos los protocolos. En versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], SPN solo se admitían en Kerberos sobre TCP cuando el valor predeterminado SPN para el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instancia se registraba en Active Directory.  
  
 Los SPN se utilizan para el protocolo de autenticación para determinar la cuenta en la que un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se ejecuta la instancia. Si se conoce la cuenta de la instancia, la autenticación Kerberos puede usarse para proporcionar una autenticación mutua del cliente y el servidor. Si no se conoce la cuenta de la instancia, se usa la autenticación NTLM, que solo proporciona autenticación del cliente por parte del servidor. Actualmente, controlador de OLE DB para SQL Server realiza la búsqueda de autenticación derivando el SPN de las propiedades de conexión de red y nombre de instancia. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] intentarán registrar los SPN al inicio, o pueden registrarse manualmente. No obstante, se producirá un error en el registro si no hay suficientes derechos de acceso para la cuenta que intenta registrar los SPN.  
  
 Las cuentas de dominio y equipo se registran automáticamente en Active Directory. Estas cuentas pueden usarse como SPN, o bien los administradores pueden definir sus propios SPN. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] hace segura de autenticación más fáciles de administrar y más confiable, permitiendo a los clientes especificar directamente el SPN que se va a usar.  
  
> [!NOTE]  
>  Un SPN especificado por una aplicación cliente solamente se utiliza cuando se establece una conexión con la seguridad integrada de Windows.  
  
> [!TIP]  
>  **[!INCLUDE[msCoName](../../../includes/msconame-md.md)] Administrador de configuración de Kerberos para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]** es una herramienta de diagnóstico que sirve para solucionar problemas de conectividad de Kerberos relacionados con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Administrador de configuración de Microsoft Kerberos para SQL Server](http://www.microsoft.com/download/details.aspx?id=39046).  
  
 Para obtener más información acerca de Kerberos, vea los siguientes artículos:  
  
-   [Complemento técnico de Kerberos para Windows](http://go.microsoft.com/fwlink/?LinkId=101449)  
  
-   [Microsoft Kerberos](http://go.microsoft.com/fwlink/?LinkID=100758)  
  
## <a name="usage"></a>Uso  
 En la tabla siguiente se describen los escenarios más comunes en los que las aplicaciones cliente pueden habilitar la autenticación segura.  
  
|Escenario|Description|  
|--------------|-----------------|  
|Una aplicación heredada no especifica ningún SPN.|Este escenario de compatibilidad garantiza que no habrá ningún cambio de comportamiento en las aplicaciones desarrolladas para versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Si no se especifica ningún SPN, la aplicación se basa en los SPN generados y no tiene ningún conocimiento del método de autenticación utilizado.|  
|Una aplicación cliente mediante la versión actual del controlador de OLE DB para SQL Server especifica un SPN en la cadena de conexión como una cuenta de usuario o equipo de dominio, como un SPN específico de la instancia o como una cadena definida por el usuario.|La palabra clave **ServerSPN** puede usarse en una cadena de conexión, inicialización o proveedor para hacer lo siguiente:<br /><br /> -Especifique la cuenta utilizada por el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instancia para una conexión. Esto simplifica el acceso a la autenticación Kerberos. Si hay presente un centro de distribución de claves Kerberos (KDC) y se especifica la cuenta correcta, es más probable que se use la autenticación Kerberos que la autenticación NTLM. El KDC reside normalmente en el mismo equipo que el controlador de dominio.<br /><br /> -Especificar un SPN para buscar la cuenta de servicio para el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instancia. Para cada [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instancia generan dos SPN predeterminados son que pueden utilizarse para este propósito. No obstante, no se garantiza que estas claves estén presentes en Active Directory, por lo que en esta situación no se garantiza la autenticación Kerberos.<br /><br /> -Especificar un SPN que se usarán para buscar la cuenta de servicio para el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instancia. Ésta puede ser cualquier cadena definida por el usuario que se asigne a la cuenta de servicio. En este caso, la clave debe registrarse manualmente en el KDC y debe cumplir las reglas de un SPN definido por el usuario.<br /><br /> La palabra clave **FailoverPartnerSPN** puede usarse para especificar el SPN para el servidor del asociado de conmutación por error. El intervalo de valores de cuenta y de clave de Active Directory es el mismo que los valores que pueden especificarse para el servidor principal.|  
|Una aplicación OLE DB especifica un SPN como una propiedad de inicialización del origen de datos para el servidor principal o para un servidor del asociado de conmutación por error.|La propiedad de conexión **SSPROP_INIT_SERVER_SPN** del conjunto de propiedades **DBPROPSET_SQLSERVERDBINIT** puede usarse para especificar el SPN de una conexión.<br /><br /> La propiedad de conexión **SSPROP_INIT_FAILOVER_PARTNER_SPN** de **DBPROPSET_SQLSERVERDBINIT** puede usarse para especificar el SPN para el servidor del asociado de conmutación por error.|   
|El usuario especifica un SPN para un servidor o servidor de asociado de conmutación por error en un cuadro de diálogo **Vínculo de datos** o **Inicio de sesión** de OLE DB.|El SPN puede especificarse en un cuadro de diálogo **Vínculo de datos** o **Inicio de sesión** .|   
|Una aplicación OLE DB determina el método de autenticación que se usa para establecer una conexión.|Cuando una conexión se ha abierto correctamente, una aplicación puede consultar la propiedad de conexión **SSPROP_AUTHENTICATION_METHOD** en el conjunto de propiedades **DBPROPSET_SQLSERVERDATASOURCEINFO** para determinar qué método de autenticación se ha utilizado. Entre los valores se incluyen **NTLM** y **Kerberos**.|  
  
## <a name="failover"></a>Conmutación por error  
 Los SPN no se almacenan en la memoria caché de conmutación por error y, por lo tanto, no pueden pasarse entre conexiones. Los SPN se usarán en todos los intentos de conexión a la entidad de seguridad y al asociado cuando se especifiquen en los atributos de cadena de conexión o atributos de conexión.  
  
## <a name="connection-pooling"></a>Agrupar conexiones  
 Las aplicaciones deben tener en cuenta que especificar los SPN en algunas cadenas de conexión, pero no en todas, pueden contribuir a la fragmentación del grupo.  
  
 Las aplicaciones pueden especificar los SPN mediante programación como atributos de conexión, en lugar de especificar las palabras clave de cadena de conexión. Esto puede contribuir a administrar la fragmentación del grupo de conexiones.  
  
 Las aplicaciones deben tener en cuenta que los SPN de las cadenas de conexión pueden invalidarse estableciendo los atributos de conexión correspondientes, pero las cadenas de conexión utilizadas por la agrupación de conexiones usarán los valores de las cadenas de conexión para los propósitos de agrupación.  
  
## <a name="down-level-server-behavior"></a>Comportamiento de un servidor de nivel inferior  
 El nuevo comportamiento de conexión lo implementa el cliente; por lo tanto, no es específico de una versión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="linked-servers-and-delegation"></a>Servidores vinculados y delegación  
 Cuando se crean servidores vinculados, el **@provstr** parámetro de [sp_addlinkedserver](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) puede utilizarse para especificar el servidor y el asociado de conmutación por error SPN. Las ventajas de hacerlo son las mismas que cuando los SPN se especifican en las cadenas de conexión del cliente: resulta más sencillo y confiable establecer conexiones que usan la autenticación Kerberos.  
  
 La delegación con servidores vinculados requiere la autenticación Kerberos.  
  
## <a name="management-aspects-of-spns-specified-by-applications"></a>Aspectos de la administración de los SPN especificados por aplicaciones  
 A la hora de decidir si debe especificar los SPN en una aplicación (a través de cadenas de conexión) o mediante programación a través de propiedades de conexión (en lugar de confiar en el proveedor predeterminado que generó los SPN), tenga en cuenta los factores siguientes:  
  
-   Seguridad: ¿el SPN especificado revela información protegida?  
  
-   Confiabilidad: Para habilitar el uso de los SPN predeterminados, la cuenta de servicio en la que el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se ejecuta la instancia debe tener suficientes privilegios para actualizar Active Directory en el KDC.  
  
-   Comodidad y transparencia de ubicación: ¿cómo afectará a los SPN de una aplicación que su base de datos se mueva a una instancia distinta de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]? Esto se aplica tanto al servidor principal como a su asociado de conmutación por error si se usa la creación de reflejo de la base de datos. Si un servidor cambia, ¿significa que deben modificarse los SPN?, ¿cómo afectará esto a las aplicaciones?, ¿se administrarán los cambios?  
  
## <a name="specifying-the-spn"></a>Especificar el SPN  
 Un SPN puede especificarse en cuadros de diálogo y en el código. En esta sección se muestra cómo especificar un SPN.  
  
 La longitud máxima de un SPN es de 260 caracteres.  
  
 La sintaxis que usan los SPN en los atributos de cadena de conexión o atributos de conexión es la siguiente:  
  
|Sintaxis|Description|  
|------------|-----------------|  
|MSSQLSvc/*fqdn*|SPN predeterminado generado por el proveedor para una instancia predeterminada cuando se usa un protocolo distinto de TCP.<br /><br /> *fqdn* es un nombre de dominio completo.|  
|MSSQLSvc/*fqdn*:*port*|SPN predeterminado generado por el proveedor cuando se usa TCP.<br /><br /> *port* es un número de puerto TCP.|  
|MSSQLSvc/*fqdn*:*InstanceName*|SPN predeterminado generado por el proveedor para una instancia con nombre cuando se usa un protocolo distinto de TCP.<br /><br /> *InstanceName* es un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nombre de instancia.|  
|HOST/*fqdn*<br /><br /> HOST/*MachineName*|SPN que se asigna a las cuentas de equipo integradas que Windows registra automáticamente.|  
|*Username*@*Domain*|Especificación directa de una cuenta de dominio.<br /><br /> *Username* es un nombre de cuenta de usuario de Windows.<br /><br /> *Domain* es un nombre de dominio de Windows o nombre de dominio completo.|  
|*MachineName*$@*Domain*|Especificación directa de una cuenta de equipo.<br /><br /> (Si el servidor al que está conectándose se ejecuta en las cuentas LOCAL SYSTEM o NETWORK SERVICE, para obtener la autenticación Kerberos, **ServerSPN** puede tener el formato *MachineName*$@*Domain* .)|  
|*KDCKey*/*MachineName*|SPN especificado por el usuario.<br /><br /> *KDCKey* es una cadena alfanumérica que se ajusta a las reglas de una clave KDC.|  
  
## <a name="ole-db-syntax-supporting-spns"></a>OLE DB sintaxis compatible con SPN  
 Para obtener información específica de la sintaxis, vea los siguientes temas:  
  
-   [Nombres principales de servicio &#40;SPN&#41; en las conexiones de cliente &#40;OLE DB&#41;](../../oledb/ole-db/service-principal-names-spns-in-client-connections-ole-db.md)  
  
 Para obtener información sobre las aplicaciones de ejemplo que muestran esta característica, vea [Ejemplos de programación de datos de SQL Server](http://msftdpprodsamples.codeplex.com/).  
  
## <a name="see-also"></a>Vea también  
 [Controlador OLE DB para características de SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)   
 [Registrar un nombre de entidad de seguridad de servicio para las conexiones con Kerberos](../../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)  
  
