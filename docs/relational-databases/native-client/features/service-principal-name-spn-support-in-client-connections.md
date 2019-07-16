---
title: Compatibilidad con nombre de entidad de seguridad de servicio (SPN) en conexiones de cliente | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client, SPNs
- ODBC, SPNs
- OLE DB, SPNs
- SPNs [SQL Server]
ms.assetid: 96598c69-ce9a-4090-aacb-d546591e8af7
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 126a419f52ee88349d1d64fcfe756fcb3681c03a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68069180"
---
# <a name="service-principal-name-spn-support-in-client-connections"></a>Compatibilidad con Nombre de la entidad de seguridad del servicio (SPN) en conexiones cliente
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  A partir de [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], se ha ampliado la compatibilidad con los nombres de entidad de seguridad de servicio (SPN) para habilitar la autenticación mutua en todos los protocolos. En versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], los SPN solo se admitían en Kerberos sobre TCP, cuando el SPN predeterminado para la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se registraba en Active Directory.  
  
 El protocolo de autenticación usa los SPN para determinar la cuenta en la que se ejecuta una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Si se conoce la cuenta de la instancia, la autenticación Kerberos puede usarse para proporcionar una autenticación mutua del cliente y el servidor. Si no se conoce la cuenta de la instancia, se usa la autenticación NTLM, que solo proporciona autenticación del cliente por parte del servidor. Actualmente, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client realiza la búsqueda de autenticación derivando el SPN de las propiedades de conexión de red y nombre de instancia. Las instancias de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] intentarán registrar los SPN al inicio, o bien pueden registrarse manualmente. No obstante, se producirá un error en el registro si no hay suficientes derechos de acceso para la cuenta que intenta registrar los SPN.  
  
 Las cuentas de dominio y equipo se registran automáticamente en Active Directory. Estas cuentas pueden usarse como SPN, o bien los administradores pueden definir sus propios SPN. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] hace que la autenticación segura sea más fácil de administrar y más confiable, ya que permite a los clientes especificar directamente el SPN que va a usarse.  
  
> [!NOTE]  
>  Un SPN especificado por una aplicación cliente solamente se utiliza cuando se establece una conexión con la seguridad integrada de Windows.  
  
> [!TIP]  
>  **[!INCLUDE[msCoName](../../../includes/msconame-md.md)] Administrador de configuración de Kerberos para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]** es una herramienta de diagnóstico que sirve para solucionar problemas de conectividad de Kerberos relacionados con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Para obtener más información, vea [Administrador de configuración de Microsoft Kerberos para SQL Server](https://www.microsoft.com/download/details.aspx?id=39046).  
  
 Para obtener más información acerca de Kerberos, vea los siguientes artículos:  
  
-   [Complemento técnico de Kerberos para Windows](https://go.microsoft.com/fwlink/?LinkId=101449)  
  
-   [Microsoft Kerberos](https://go.microsoft.com/fwlink/?LinkID=100758)  
  
## <a name="usage"></a>Uso  
 En la tabla siguiente se describen los escenarios más comunes en los que las aplicaciones cliente pueden habilitar la autenticación segura.  
  
|Escenario|Descripción|  
|--------------|-----------------|  
|Una aplicación heredada no especifica ningún SPN.|Este escenario de compatibilidad garantiza que no habrá ningún cambio de comportamiento en las aplicaciones desarrolladas para versiones anteriores de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Si no se especifica ningún SPN, la aplicación se basa en los SPN generados y no tiene ningún conocimiento del método de autenticación utilizado.|  
|Una aplicación cliente que usa la versión actual de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client especifica un SPN en la cadena de conexión como un usuario de dominio o cuenta de equipo, como un SPN específico de la instancia o como una cadena definida por el usuario.|La palabra clave **ServerSPN** puede usarse en una cadena de conexión, inicialización o proveedor para hacer lo siguiente:<br /><br /> \- Especificar la cuenta usada por la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para una conexión. Esto simplifica el acceso a la autenticación Kerberos. Si hay presente un centro de distribución de claves Kerberos (KDC) y se especifica la cuenta correcta, es más probable que se use la autenticación Kerberos que la autenticación NTLM. El KDC reside normalmente en el mismo equipo que el controlador de dominio.<br /><br /> \- Especificar un SPN para buscar la cuenta de servicio para la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Por cada instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], se generan dos SPN predeterminados que pueden usarse para este propósito. No obstante, no se garantiza que estas claves estén presentes en Active Directory, por lo que en esta situación no se garantiza la autenticación Kerberos.<br /><br /> \- Especificar un SPN que se usará para buscar la cuenta de servicio para la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Ésta puede ser cualquier cadena definida por el usuario que se asigne a la cuenta de servicio. En este caso, la clave debe registrarse manualmente en el KDC y debe cumplir las reglas de un SPN definido por el usuario.<br /><br /> La palabra clave **FailoverPartnerSPN** puede usarse para especificar el SPN para el servidor del asociado de conmutación por error. El intervalo de valores de cuenta y de clave de Active Directory es el mismo que los valores que pueden especificarse para el servidor principal.|  
|Una aplicación ODBC especifica un SPN como un atributo de conexión para el servidor principal o servidor del asociado de conmutación por error.|El atributo de conexión **SQL_COPT_SS_SERVER_SPN** puede usarse para especificar el SPN de una conexión al servidor principal.<br /><br /> El atributo de conexión **SQL_COPT_SS_FAILOVER_PARTNER_SPN** puede usarse para especificar el SPN para el servidor del asociado de conmutación por error.|  
|Una aplicación OLE DB especifica un SPN como una propiedad de inicialización del origen de datos para el servidor principal o para un servidor del asociado de conmutación por error.|La propiedad de conexión **SSPROP_INIT_SERVER_SPN** del conjunto de propiedades **DBPROPSET_SQLSERVERDBINIT** puede usarse para especificar el SPN de una conexión.<br /><br /> La propiedad de conexión **SSPROP_INIT_FAILOVER_PARTNER_SPN** de **DBPROPSET_SQLSERVERDBINIT** puede usarse para especificar el SPN para el servidor del asociado de conmutación por error.|  
|Un usuario especifica un SPN para un servidor o servidor de asociado de conmutación por error en un nombre del origen de datos ODBC (DSN).|El SPN puede especificarse en un DSN ODBC a través de los cuadros de diálogo de configuración del DSN.|  
|El usuario especifica un SPN para un servidor o servidor de asociado de conmutación por error en un cuadro de diálogo **Vínculo de datos** o **Inicio de sesión** de OLE DB.|El SPN puede especificarse en un cuadro de diálogo **Vínculo de datos** o **Inicio de sesión** . El cuadro de diálogo **Inicio de sesión** puede usarse con ODBC u OLE DB.|  
|Una aplicación ODBC determina el método de autenticación que se usa para establecer una conexión.|Cuando una conexión se ha abierto correctamente, una aplicación puede consultar el atributo de conexión **SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD** para determinar qué método de autenticación se ha utilizado. Entre los valores se incluyen **NTLM** y **Kerberos**.|  
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
 Cuando se crean servidores vinculados, el parámetro **@provstr** de [sp_addlinkedserver](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md) puede usarse para especificar los SPN del servidor y del asociado de conmutación por error. Las ventajas de hacer esto son las mismas de especificar los SPN en las cadenas de conexión de cliente: Es más sencillo y confiable establecer conexiones que usan la autenticación Kerberos.  
  
 La delegación con servidores vinculados requiere la autenticación Kerberos.  
  
## <a name="management-aspects-of-spns-specified-by-applications"></a>Aspectos de la administración de los SPN especificados por aplicaciones  
 A la hora de decidir si debe especificar los SPN en una aplicación (a través de cadenas de conexión) o mediante programación a través de propiedades de conexión (en lugar de confiar en el proveedor predeterminado que generó los SPN), tenga en cuenta los factores siguientes:  
  
-   Seguridad: ¿El SPN especificado revela información protegida?  
  
-   Confiabilidad: Para habilitar el uso de los SPN de forma predeterminada, la cuenta de servicio en la que el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se ejecuta la instancia debe tener suficientes privilegios para actualizar Active Directory en el KDC.  
  
-   Comodidad y transparencia de ubicación: ¿Cómo de la aplicación afectará a los SPN si su base de datos se mueve a otro [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instancia? Esto se aplica tanto al servidor principal como a su asociado de conmutación por error si se usa la creación de reflejo de la base de datos. Si un servidor cambia, ¿significa que deben modificarse los SPN?, ¿cómo afectará esto a las aplicaciones?, ¿se administrarán los cambios?  
  
## <a name="specifying-the-spn"></a>Especificar el SPN  
 Un SPN puede especificarse en cuadros de diálogo y en el código. En esta sección se muestra cómo especificar un SPN.  
  
 La longitud máxima de un SPN es de 260 caracteres.  
  
 La sintaxis que usan los SPN en los atributos de cadena de conexión o atributos de conexión es la siguiente:  
  
|Sintaxis|Descripción|  
|------------|-----------------|  
|MSSQLSvc/*fqdn*|SPN predeterminado generado por el proveedor para una instancia predeterminada cuando se usa un protocolo distinto de TCP.<br /><br /> *fqdn* es un nombre de dominio completo.|  
|MSSQLSvc/*fqdn*:*port*|SPN predeterminado generado por el proveedor cuando se usa TCP.<br /><br /> *port* es un número de puerto TCP.|  
|MSSQLSvc/*fqdn*:*InstanceName*|SPN predeterminado generado por el proveedor para una instancia con nombre cuando se usa un protocolo distinto de TCP.<br /><br /> *InstanceName* es un nombre de instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|HOST/*fqdn*<br /><br /> HOST/*MachineName*|SPN que se asigna a las cuentas de equipo integradas que Windows registra automáticamente.|  
|*Username*@*Domain*|Especificación directa de una cuenta de dominio.<br /><br /> *Username* es un nombre de cuenta de usuario de Windows.<br /><br /> *Domain* es un nombre de dominio de Windows o nombre de dominio completo.|  
|*MachineName*$@*Domain*|Especificación directa de una cuenta de equipo.<br /><br /> (Si el servidor al que está conectándose se ejecuta en las cuentas LOCAL SYSTEM o NETWORK SERVICE, para obtener la autenticación Kerberos, **ServerSPN** puede tener el formato *MachineName*$@*Domain* .)|  
|*KDCKey*/*MachineName*|SPN especificado por el usuario.<br /><br /> *KDCKey* es una cadena alfanumérica que se ajusta a las reglas de una clave KDC.|  
  
## <a name="odbc-and-ole-db-syntax-supporting-spns"></a>Sintaxis de ODBC y OLE DB compatible con los SPN  
 Para obtener información específica de la sintaxis, vea los siguientes temas:  
  
-   [Los nombres de entidad de servicio &#40;SPN&#41; en conexiones cliente &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)  
  
-   [Nombres de entidad de seguridad de servicio &#40;SPN&#41; en conexiones de cliente &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/service-principal-names-spns-in-client-connections-ole-db.md)  
  
 Para obtener información sobre las aplicaciones de ejemplo que muestran esta característica, vea [Ejemplos de programación de datos de SQL Server](https://msftdpprodsamples.codeplex.com/).  
  
## <a name="see-also"></a>Vea también  
 [Características de SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
[Registrar un nombre principal de servicio para las conexiones con Kerberos](../../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)  
  
