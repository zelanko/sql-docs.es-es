---
title: ALTER ROUTE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_ROUTE_TSQL
- ALTER ROUTE
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER ROUTE statement
- dropping routes
- modifying routes
- removing routes
- routes [Service Broker], modifying
ms.assetid: 8dfb7b16-3dac-4e1e-8c97-adf2aad07830
caps.latest.revision: 33
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 39e39b8688e2350d27e664b4a1517584c11df941
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="alter-route-transact-sql"></a>ALTER ROUTE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Modifica la información de ruta de una ruta existente en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ALTER ROUTE route_name  
WITH    
  [ SERVICE_NAME = 'service_name' [ , ] ]  
  [ BROKER_INSTANCE = 'broker_instance' [ , ] ]  
  [ LIFETIME = route_lifetime [ , ] ]  
  [ ADDRESS =  'next_hop_address' [ , ] ]  
  [ MIRROR_ADDRESS = 'next_hop_mirror_address' ]  
[ ; ]  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *route_name*  
 Es el nombre de la ruta que se va a cambiar. No se pueden especificar nombres de servidor, base de datos o esquema.  
  
 por  
 Presenta las cláusulas que definen la ruta que se va a modificar.  
  
 SERVICE_NAME **='***service_name***'**  
 Especifica el nombre del servicio remoto señalado por esta ruta. El *service_name* debe coincidir exactamente con el nombre de servicio remoto utiliza. [!INCLUDE[ssSB](../../includes/sssb-md.md)]utiliza una comparación byte a byte para que coincida con el *service_name*. En otras palabras, en la comparación se distinguen mayúsculas y minúsculas, y no se considera la intercalación actual. Una ruta con un nombre de servicio de **' SQL/ServiceBroker/BrokerConfiguration'** es una ruta a un servicio de notificación de configuración de Service Broker. Es posible que una ruta a este servicio no especifique una instancia de agente.  
  
 Si se omite la cláusula SERVICE_NAME, el nombre de servicio de la ruta no varía.  
  
 BROKER_INSTANCE **='***broker_instance***'**  
 Especifica la base de datos que hospeda el servicio de destino. El *broker_instance* parámetro debe ser el identificador de instancia de broker para la base de datos remoto, que puede obtenerse mediante la ejecución de la consulta siguiente en la base de datos seleccionada:  
  
```  
SELECT service_broker_guid  
FROM sys.databases  
WHERE database_id = DB_ID();  
```  
  
 Si se omite la cláusula BROKER_INSTANCE, la instancia de broker para la ruta no varía.  
  
> [!NOTE]  
>  Esta opción no está disponible en las bases de datos independientes.  
  
 DURACIÓN  **=**  *route_lifetime*  
 Especifica el tiempo, en segundos, durante el que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retiene la ruta en la tabla de enrutamiento. Transcurrido este tiempo, la ruta expira y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ya no la tiene en cuenta al elegir una ruta para una conversación nueva. Si se omite esta cláusula, la vigencia de la ruta no varía.  
  
 DIRECCIÓN **='***next_hop_address'*  
 Especifica la dirección de red para esta ruta. El *next_hop_address* especifica una dirección TCP/IP en el formato siguiente:  
  
 **TCP: / /** { *dns_name* | *nombreNetBIOS* |*dirección_IP* } **:**  *número_puerto*  
  
 Especificado *port_number* debe coincidir con el número de puerto para el [!INCLUDE[ssSB](../../includes/sssb-md.md)] punto de conexión de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el equipo especificado. Se puede obtener ejecutando la consulta siguiente en la base de datos seleccionada:  
  
```  
SELECT tcpe.port  
FROM sys.tcp_endpoints AS tcpe  
INNER JOIN sys.service_broker_endpoints AS ssbe  
   ON ssbe.endpoint_id = tcpe.endpoint_id  
WHERE ssbe.name = N'MyServiceBrokerEndpoint';  
```  
  
 Cuando se especifica una ruta **'LOCAL'** para el *next_hop_address*, el mensaje se entrega a un servicio en la instancia actual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Cuando se especifica una ruta **'TRANSPORT'** para el *next_hop_address*, la dirección de red se determina en función de la dirección de red el nombre del servicio. Una ruta que especifica **'TRANSPORT'** puede especificar una instancia de service broker o de nombre.  
  
 Cuando el *next_hop_address* es el servidor principal para una base de datos reflejada, debe especificar también MIRROR_ADDRESS para el servidor reflejado. En caso contrario, esta ruta no realiza la conmutación por error automáticamente al servidor reflejado.  
  
> [!NOTE]  
>  Esta opción no está disponible en las bases de datos independientes.  
  
 MIRROR_ADDRESS **='***next_hop_mirror_address***'**  
 Especifica la dirección de red para el servidor reflejado de un par reflejado cuyo servidor principal está en el *next_hop_address*. El *next_hop_mirror_address* especifica una dirección TCP/IP en el formato siguiente:  
  
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
  
> [!NOTE]  
>  Esta opción no está disponible en las bases de datos independientes.  
  
## <a name="remarks"></a>Comentarios  
 La tabla de enrutamiento que almacena las rutas es una tabla de metadatos que se pueden leer a través de la **sys.routes** vista de catálogo. La tabla de enrutamiento solo se puede actualizar mediante las instrucciones CREATE ROUTE, ALTER ROUTE y DROP ROUTE.  
  
 Las cláusulas que no se especifican en el comando ALTER ROUTE no varían. Por consiguiente, no se puede aplicar ALTER a una ruta para especificar que dicha ruta no agota el tiempo de espera, que coincide con un nombre de servicio o que coincide con una instancia de agente. Para cambiar estas características de la ruta, debe quitar la ruta existente y crear otra ruta con la información nueva.  
  
 Cuando se especifica una ruta **'TRANSPORT'** para el *next_hop_address*, la dirección de red se determina según el nombre del servicio. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]puede procesar correctamente los nombres de servicio que comienzan con una dirección de red en un formato que sea válido para un *next_hop_address*. Los servicios con nombres que contienen direcciones de red válidas se enrutan a la dirección de red del nombre de servicio.  
  
 La tabla de enrutamiento puede contener un número indeterminado de rutas que especifican el mismo servicio, dirección de red e identificador de instancia de broker. En este caso, [!INCLUDE[ssSB](../../includes/sssb-md.md)] elige una ruta mediante un procedimiento diseñado para buscar la coincidencia más exacta entre la información especificada en la conversación y la información de la tabla de enrutamiento.  
  
 Para modificar AUTHORIZATION para un servicio, utilice la instrucción ALTER AUTHORIZATION.  
  
## <a name="permissions"></a>Permissions  
 Permiso para modificar una ruta de forma predeterminada el propietario de la ruta, los miembros de la **db_ddladmin** o **db_owner** se han corregido los roles de base de datos y los miembros de la **sysadmin** fijo rol de servidor.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-changing-the-service-for-a-route"></a>A. Cambiar el servicio para una ruta  
 En el ejemplo siguiente se modifica la ruta `ExpenseRoute` para que señale al servicio remoto `//Adventure-Works.com/Expenses`.  
  
```  
ALTER ROUTE ExpenseRoute  
   WITH   
     SERVICE_NAME = '//Adventure-Works.com/Expenses';  
```  
  
### <a name="b-changing-the-target-database-for-a-route"></a>B. Cambiar la base de datos de destino para una ruta  
 En el ejemplo siguiente se cambia la base de datos de destino para la ruta `ExpenseRoute` a la base de datos identificada por el identificador único `D8D4D268-00A3-4C62-8F91-634B89B1E317.`  
  
```  
ALTER ROUTE ExpenseRoute  
   WITH   
     BROKER_INSTANCE = 'D8D4D268-00A3-4C62-8F91-634B89B1E317';  
```  
  
### <a name="c-changing-the-address-for-a-route"></a>C. Cambiar la dirección para una ruta  
 En el ejemplo siguiente se cambia la dirección de red para la ruta `ExpenseRoute` al puerto TCP `1234` en el host con la dirección IP `10.2.19.72`.  
  
```  
ALTER ROUTE ExpenseRoute   
   WITH   
     ADDRESS = 'TCP://10.2.19.72:1234';  
```  
  
### <a name="d-changing-the-database-and-address-for-a-route"></a>D. Cambiar la base de datos y la dirección para una ruta  
 En el ejemplo siguiente se cambia la dirección de red para la ruta `ExpenseRoute` al puerto TCP `1234` en el host con el nombre DNS `www.Adventure-Works.com`. También se cambia la base de datos de destino a la base de datos identificada por el identificador único `D8D4D268-00A3-4C62-8F91-634B89B1E317`.  
  
```  
ALTER ROUTE ExpenseRoute  
   WITH   
     BROKER_INSTANCE = 'D8D4D268-00A3-4C62-8F91-634B89B1E317',  
     ADDRESS = 'TCP://www.Adventure-Works.com:1234';  
```  
  
## <a name="see-also"></a>Vea también  
 [CREATE ROUTE &#40;Transact-SQL&#41;](../../t-sql/statements/create-route-transact-sql.md)   
 [DROP ROUTE &#40; Transact-SQL &#41;](../../t-sql/statements/drop-route-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
