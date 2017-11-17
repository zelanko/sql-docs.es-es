---
title: Crear ruta (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_ROUTE_TSQL
- ROUTE
- CREATE ROUTE
- ROUTE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- lifetimes [Service Broker]
- routes [Service Broker], creating
- forwarding brokers [SQL Server]
- service names [Service Broker]
- database mirroring [SQL Server], routing
- expired routes [SQL Server]
- activating routes
- CREATE ROUTE statement
ms.assetid: 7e695364-1a98-4cfd-8ebd-137ac5a425b3
caps.latest.revision: 42
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b7268b5c9b43505d3c66fb6573a9a41c3cd62e3a
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-route-transact-sql"></a>CREATE ROUTE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Agrega una ruta nueva a la tabla de enrutamiento para la base de datos actual. Para los mensajes salientes, [!INCLUDE[ssSB](../../includes/sssb-md.md)] determina el enrutamiento mediante la comprobación de la tabla de enrutamiento en la base de datos local. Para los mensajes en las conversaciones que se originan en otra instancia, incluidos los mensajes que se reenvían, [!INCLUDE[ssSB](../../includes/sssb-md.md)] comprueba las rutas en **msdb**.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CREATE ROUTE route_name  
[ AUTHORIZATION owner_name ]  
WITH    
   [ SERVICE_NAME = 'service_name', ]  
   [ BROKER_INSTANCE = 'broker_instance_identifier' , ]  
   [ LIFETIME = route_lifetime , ]  
   ADDRESS =  'next_hop_address'  
   [ , MIRROR_ADDRESS = 'next_hop_mirror_address' ]  
[ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *route_name*  
 Es el nombre de la ruta que se va a crear. Se crea una ruta nueva en la base de datos actual, la cual pertenece a la entidad de seguridad especificada en la cláusula AUTHORIZATION. No se pueden especificar nombres de servidor, base de datos o esquema. El *route_name* debe ser válido **sysname**.  
  
 AUTORIZACIÓN *owner_name*  
 Establece el propietario de la ruta en el usuario o el rol de base de datos que se ha especificado. El *owner_name* puede ser el nombre de cualquier usuario o rol válidos cuando el usuario actual es miembro de la **db_owner** rol fijo de base de datos o la **sysadmin** rol fijo de servidor. En caso contrario, *owner_name* debe ser el nombre del usuario actual, el nombre de un usuario que el usuario actual tiene permiso IMPERSONATE o el nombre de un rol al que pertenece el usuario actual. Si se omite esta cláusula, la ruta pertenece al usuario actual.  
  
 por  
 Presenta las cláusulas que definen la ruta creada.  
  
 SERVICE_NAME = **'***service_name***'**  
 Especifica el nombre del servicio remoto señalado por esta ruta. El *service_name* debe coincidir exactamente con el nombre de servicio remoto utiliza. [!INCLUDE[ssSB](../../includes/sssb-md.md)]utiliza una comparación byte a byte para que coincida con el *service_name*. En otras palabras, en la comparación se distinguen mayúsculas y minúsculas, y no se considera la intercalación actual. Si se omite SERVICE_NAME, esta ruta coincide con todos los nombres de servicio, pero tiene una prioridad inferior de coincidencia con respecto a una ruta que especifique SERVICE_NAME. Una ruta con un nombre de servicio de **' SQL/ServiceBroker/BrokerConfiguration'** es una ruta a un servicio de notificación de configuración de Service Broker. Es posible que una ruta a este servicio no especifique una instancia de agente.  
  
 BROKER_INSTANCE = **'***broker_instance_identifier***'**  
 Especifica la base de datos que hospeda el servicio de destino. El *broker_instance_identifier* parámetro debe ser el identificador de instancia de broker para la base de datos remoto, que puede obtenerse mediante la ejecución de la consulta siguiente en la base de datos seleccionada:  
  
```  
SELECT service_broker_guid  
FROM sys.databases  
WHERE database_id = DB_ID()  
```  
  
 Si se omite la cláusula BROKER_INSTANCE, esta ruta coincide con todas las instancias de agente. Una ruta que coincida con todas las instancias de agente tiene una prioridad superior de coincidencia con respecto a las rutas con una instancia de agente explícita si la conversación no especifica una instancia de broker. Para las conversaciones que especifican una instancia de agente, una ruta con una instancia de agente tiene una prioridad superior a la de una ruta que coincida con todas las instancias de agente.  
  
 DURACIÓN  **=**  *route_lifetime*  
 Especifica el tiempo, en segundos, durante el que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retiene la ruta en la tabla de enrutamiento. Transcurrido este tiempo, la ruta expira y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ya no la tiene en cuenta al elegir una ruta para una conversación nueva. Si se omite esta cláusula, el *route_lifetime* es NULL y la ruta no expira nunca.  
  
 DIRECCIÓN **='***next_hop_address***'**  
 Especifica la dirección de red para esta ruta. El *next_hop_address* especifica una dirección TCP/IP en el formato siguiente:  
  
 **TCP: / /**{ *dns_name* | *nombreNetBIOS* | *dirección_IP* } **:**  *número_puerto*  
  
 Especificado *port_number* debe coincidir con el número de puerto para el [!INCLUDE[ssSB](../../includes/sssb-md.md)] punto de conexión de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el equipo especificado. Se puede obtener ejecutando la consulta siguiente en la base de datos seleccionada:  
  
```  
SELECT tcpe.port  
FROM sys.tcp_endpoints AS tcpe  
INNER JOIN sys.service_broker_endpoints AS ssbe  
   ON ssbe.endpoint_id = tcpe.endpoint_id  
WHERE ssbe.name = N'MyServiceBrokerEndpoint';  
```  
  
 Si el servicio se hospeda en una base de datos reflejada, debe especificar también MIRROR_ADDRESS para la otra instancia que hospeda una base de datos reflejada. En caso contrario, esta ruta no realiza la conmutación por error al reflejo.  
  
 Cuando se especifica una ruta **'LOCAL'** para el *next_hop_address*, el mensaje se entrega a un servicio en la instancia actual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Cuando se especifica una ruta **'TRANSPORT'** para el *next_hop_address*, la dirección de red se determina en función de la dirección de red el nombre del servicio. Una ruta que especifica **'TRANSPORT'** no se puede especificar una instancia del nombre o un agente de servicio.  
  
 MIRROR_ADDRESS **='***next_hop_mirror_address***'**  
 Especifica la dirección de red para una base de datos reflejada con una base de datos reflejada hospedada en la *next_hop_address*. El *next_hop_mirror_address* especifica una dirección TCP/IP en el formato siguiente:  
  
 **TCP: / /**{ *dns_name* | *nombreNetBIOS* | *dirección_IP* } **:**  *número_puerto*  
  
 Especificado *port_number* debe coincidir con el número de puerto para el [!INCLUDE[ssSB](../../includes/sssb-md.md)] punto de conexión de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el equipo especificado. Se puede obtener ejecutando la consulta siguiente en la base de datos seleccionada:  
  
```  
SELECT tcpe.port  
FROM sys.tcp_endpoints AS tcpe  
INNER JOIN sys.service_broker_endpoints AS ssbe  
   ON ssbe.endpoint_id = tcpe.endpoint_id  
WHERE ssbe.name = N'MyServiceBrokerEndpoint';  
```  
  
 Si se especifica MIRROR_ADDRESS, la ruta debe especificar la cláusula SERVICE_NAME y la cláusula BROKER_INSTANCE. Una ruta que especifica **'LOCAL'** o **'TRANSPORT'** para el *next_hop_address* no se puede especificar una dirección de reflejo.  
  
## <a name="remarks"></a>Comentarios  
 La tabla de enrutamiento que almacena las rutas es una tabla de metadatos que se pueden leer a través de la **sys.routes** vista de catálogo. Esta vista de catálogo solo se puede actualizar mediante las instrucciones CREATE ROUTE, ALTER ROUTE y DROP ROUTE.  
  
 De forma predeterminada, la tabla de enrutamiento de cada base de datos de usuario contiene una ruta. Esta ruta se denomina **AutoCreatedLocal**. Especifica la ruta **'LOCAL'** para el *next_hop_address* y coincide con cualquier identificador de la instancia de broker y el nombre del servicio.  
  
 Cuando se especifica una ruta **'TRANSPORT'** para el *next_hop_address*, la dirección de red se determina según el nombre del servicio. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]puede procesar correctamente los nombres de servicio que comienzan con una dirección de red en un formato que sea válido para un *next_hop_address*.  
  
 La tabla de enrutamiento puede contener un número indeterminado de rutas que especifican el mismo servicio, dirección de red e identificador de instancia de agente. En este caso, [!INCLUDE[ssSB](../../includes/sssb-md.md)] elige una ruta mediante un procedimiento diseñado para buscar la coincidencia más exacta entre la información especificada en la conversación y la información de la tabla de enrutamiento.  
  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] no quita las rutas expiradas de la tabla de enrutamiento. Se puede activar una ruta expirada mediante la instrucción ALTER ROUTE.  
  
 Una ruta no puede ser un objeto temporal. Enrutar nombres que empiezan por  **#**  se permiten, pero son objetos permanentes.  
  
## <a name="permissions"></a>Permissions  
 Permiso para crear una ruta de forma predeterminada a los miembros de la **db_ddladmin** o **db_owner** funciones fijas de base de datos y la **sysadmin** rol fijo de servidor.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-creating-a-tcpip-route-by-using-a-dns-name"></a>A. Crear una ruta TCP/IP con un nombre DNS  
 En el ejemplo siguiente se crea una ruta al servicio `//Adventure-Works.com/Expenses`. La ruta especifica que los mensajes para este servicio se desplazan por TCP hasta el puerto `1234` del host identificado mediante el nombre DNS `www.Adventure-Works.com`. Al llegar los mensajes, el servidor de destino los entrega a la instancia de agente indicada mediante el identificador único `D8D4D268-00A3-4C62-8F91-634B89C1E315`.  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    BROKER_INSTANCE = 'D8D4D268-00A3-4C62-8F91-634B89C1E315',  
    ADDRESS = 'TCP://www.Adventure-Works.com:1234' ;  
```  
  
### <a name="b-creating-a-tcpip-route-by-using-a-netbios-name"></a>B. Crear una ruta TCP/IP con un nombre NetBIOS  
 En el ejemplo siguiente se crea una ruta al servicio `//Adventure-Works.com/Expenses`. La ruta especifica que los mensajes para este servicio se desplazan por TCP hasta el puerto `1234` del host identificado mediante el nombre NetBIOS `SERVER02`. Cuando llega el mensaje, la sesión de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lo entrega a la instancia de base de datos indicada por el identificador único `D8D4D268-00A3-4C62-8F91-634B89C1E315`.  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH   
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    BROKER_INSTANCE = 'D8D4D268-00A3-4C62-8F91-634B89C1E315',  
    ADDRESS = 'TCP://SERVER02:1234' ;  
```  
  
### <a name="c-creating-a-tcpip-route-by-using-an-ip-address"></a>C. Crear una ruta TCP/IP con una dirección IP  
 En el ejemplo siguiente se crea una ruta al servicio `//Adventure-Works.com/Expenses`. La ruta especifica que los mensajes para este servicio se desplazan por TCP hasta el puerto `1234` del host en la dirección IP `192.168.10.2`. Cuando llega el mensaje, la sesión de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] lo entrega a la instancia de agente indicada por el identificador único `D8D4D268-00A3-4C62-8F91-634B89C1E315`.  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    BROKER_INSTANCE = 'D8D4D268-00A3-4C62-8F91-634B89C1E315',  
    ADDRESS = 'TCP://192.168.10.2:1234' ;  
```  
  
### <a name="d-creating-a-route-to-a-forwarding-broker"></a>D. Crear una ruta a un agente de reenvío  
 En el ejemplo siguiente se crea una ruta al agente de reenvío en el servidor `dispatch.Adventure-Works.com`. Dado que no se especifica el nombre de servicio ni el identificador de la instancia de agente, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa esta ruta para los servicios que no tienen ninguna otra ruta definida.  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    ADDRESS = 'TCP://dispatch.Adventure-Works.com' ;   
```  
  
### <a name="e-creating-a-route-to-a-local-service"></a>E. Crear una ruta a un servicio local  
 En el ejemplo siguiente se crea una ruta al servicio `//Adventure-Works.com/LogRequests` en la misma instancia que la ruta.  
  
```  
CREATE ROUTE LogRequests  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/LogRequests',  
    ADDRESS = 'LOCAL' ;  
```  
  
### <a name="f-creating-a-route-with-a-specified-lifetime"></a>F. Crear una ruta con una duración específica  
 En el ejemplo siguiente se crea una ruta al servicio `//Adventure-Works.com/Expenses`. La duración de la ruta es `259200` segundos, lo que equivale a 72 horas.  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    LIFETIME = 259200,  
    ADDRESS = 'TCP://services.Adventure-Works.com:1234' ;  
```  
  
### <a name="g-creating-a-route-to-a-mirrored-database"></a>G. Crear una ruta a una base de datos reflejada  
 En el ejemplo siguiente se crea una ruta al servicio `//Adventure-Works.com/Expenses`. El servicio se hospeda en una base de datos reflejada. Una de las bases de datos reflejadas se encuentra en la dirección `services.Adventure-Works.com:1234` y la otra en la dirección `services-mirror.Adventure-Works.com:1234`.  
  
```  
CREATE ROUTE ExpenseRoute  
    WITH  
    SERVICE_NAME = '//Adventure-Works.com/Expenses',  
    BROKER_INSTANCE = '69fcc80c-2239-4700-8437-1001ecddf933',  
    ADDRESS = 'TCP://services.Adventure-Works.com:1234',   
    MIRROR_ADDRESS = 'TCP://services-mirror.Adventure-Works.com:1234' ;  
```  
  
### <a name="h-creating-a-route-that-uses-the-service-name-for-routing"></a>H. Crear una ruta que utiliza el nombre de servicio para el enrutamiento  
 En el siguiente ejemplo se crea una ruta que utiliza el nombre del servicio para determinar la dirección de red a la que se va a enviar el mensaje. Tenga en cuenta que una ruta que especifica `'TRANSPORT'` como dirección de red tiene una prioridad inferior de coincidencia con respecto al resto de las rutas.  
  
```  
CREATE ROUTE TransportRoute  
    WITH ADDRESS = 'TRANSPORT' ;  
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER ROUTE &#40; Transact-SQL &#41;](../../t-sql/statements/alter-route-transact-sql.md)   
 [DROP ROUTE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-route-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  

