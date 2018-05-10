---
title: Sys.dm_broker_connections (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/08/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_broker_connections
- dm_broker_connections
- sys.dm_broker_connections_TSQL
- dm_broker_connections_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_broker_connections dynamic management view
ms.assetid: d9e20433-67fe-4fcc-80e3-b94335b2daef
caps.latest.revision: 45
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ba07b39c517c07d26a2565b2b447848f82a95b9d
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmbrokerconnections-transact-sql"></a>sys.dm_broker_connections (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila por cada conexión de red de [!INCLUDE[ssSB](../../includes/sssb-md.md)]. En la tabla siguiente se proporciona más información:  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**connection_id**|**uniqueidentifier**|Identificador de la conexión. ACEPTA VALORES NULL.|  
|**transport_stream_id**|**uniqueidentifier**|Identificador de la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conexión de interfaz de red (SNI) utilizado por esta conexión para las comunicaciones TCP/IP. ACEPTA VALORES NULL.|  
|**state**|**smallint**|Estado actual de la conexión. ACEPTA VALORES NULL. Valores posibles:<br /><br /> 1 = NEW<br /><br /> 2 = CONNECTING<br /><br /> 3 = CONNECTED<br /><br /> 4 = LOGGED_IN<br /><br /> 5 = CERRADO|  
|**state_desc**|**nvarchar(60)**|Estado actual de la conexión. ACEPTA VALORES NULL. Valores posibles:<br /><br /> NEW<br /><br /> CONNECTING<br /><br /> CONNECTED<br /><br /> LOGGED_IN<br /><br /> CLOSED|  
|**connect_time**|**datetime**|Fecha y hora a la que se inició la conexión. ACEPTA VALORES NULL.|  
|**login_time**|**datetime**|Fecha y hora a la que se inició una sesión correctamente para la conexión. ACEPTA VALORES NULL.|  
|**authentication_method**|**nvarchar(128)**|Nombre del método de autenticación de Windows, como por ejemplo NTLM o KERBEROS. Este valor proviene de Windows. ACEPTA VALORES NULL.|  
|**principal_name**|**nvarchar(128)**|Nombre de inicio de sesión que fue validado para obtener permiso de conexión. En el caso de la autenticación de Windows, este valor es el nombre del usuario remoto. En el caso de autenticación basada en certificados, este valor es el propietario del certificado. ACEPTA VALORES NULL.|  
|**remote_user_name**|**nvarchar(128)**|Nombre del usuario del mismo nivel en la otra base de datos utilizado por la Autenticación de Windows. ACEPTA VALORES NULL.|  
|**last_activity_time**|**datetime**|Fecha y hora a la que se utilizó la conexión por última vez para enviar o recibir información. ACEPTA VALORES NULL.|  
|**is_accept**|**bit**|Indica si la conexión se originó en el lado remoto. ACEPTA VALORES NULL.<br /><br /> 1 = La conexión es una solicitud aceptada por la instancia remota.<br /><br /> 0 = La conexión fue iniciada por la instancia local.|  
|**login_state**|**smallint**|Estado del proceso de inicio de sesión de esta conexión. Valores posibles:<br /><br /> 0 = INITIAL<br /><br /> 1 = WAIT LOGIN NEGOTIATE<br /><br /> 2 = ONE ISC<br /><br /> 3 = ONE ASC<br /><br /> 4 = TWO ISC<br /><br /> 5 = TWO ASC<br /><br /> 6 = WAIT ISC Confirm<br /><br /> 7 = WAIT ASC Confirm<br /><br /> 8 = WAIT REJECT<br /><br /> 9 = WAIT PRE-MASTER SECRET<br /><br /> 10 = WAIT VALIDATION<br /><br /> 11 = WAIT ARBITRATION<br /><br /> 12 = EN LÍNEA<br /><br /> 13 = ERROR|  
|**login_state_desc**|**nvarchar(60)**|Estado actual del inicio de sesión en el equipo remoto. Valores posibles:<br /><br /> Se está inicializando el protocolo de enlace de la conexión.<br /><br /> El protocolo de enlace de la conexión está esperando el mensaje de negociación de inicio de sesión.<br /><br /> El protocolo de enlace de la conexión se ha inicializado y ha enviado el contexto de seguridad para la autenticación.<br /><br /> El protocolo de enlace de la conexión ha recibido y aceptado el contexto de seguridad para la autenticación.<br /><br /> El protocolo de enlace de la conexión se ha inicializado y ha enviado el contexto de seguridad para la autenticación. Existe un mecanismo opcional disponible para la autenticación de los elementos del mismo nivel.<br /><br /> El protocolo de enlace de la conexión ha recibido y enviado el contexto de seguridad aceptado para la autenticación. Existe un mecanismo opcional disponible para la autenticación de los elementos del mismo nivel.<br /><br /> El protocolo de enlace de la conexión está esperando el mensaje de confirmación de inicialización del contexto de seguridad.<br /><br /> El protocolo de enlace de la conexión está esperando el mensaje de confirmación de aceptación del contexto de seguridad.<br /><br /> El protocolo de enlace de la conexión está esperando el mensaje de rechazo de SSPI para un error de autenticación.<br /><br /> El protocolo de enlace de la conexión está esperando el mensaje de secreto maestro preliminar.<br /><br /> El protocolo de enlace de la conexión está esperando el mensaje de validación.<br /><br /> El protocolo de enlace de la conexión está esperando el mensaje de arbitraje.<br /><br /> El protocolo en enlace de la conexión está completado y en línea (listo) para el intercambio de mensajes.<br /><br /> La conexión tiene errores.|  
|**peer_certificate_id**|**int**|El identificador del objeto local del certificado que utiliza la instancia remota para la autenticación. El propietario de este certificado debe tener permisos CONNECT para el extremo de [!INCLUDE[ssSB](../../includes/sssb-md.md)]. ACEPTA VALORES NULL.|  
|**encryption_algorithm**|**smallint**|Algoritmo de cifrado utilizado para esta conexión. ACEPTA VALORES NULL. Valores posibles:<br /><br /> **Valor &#124; descripción &#124; opción DDL correspondiente**<br /><br /> 0 &#124; ninguno &#124; deshabilitado<br /><br /> 1 &AMP;#124; FIRMA SÓLO<br /><br /> 2 &#124; AES, RC4 &#124; requiere &#124; necesita el algoritmo RC4}<br /><br /> 3 &#124; AES &#124;necesita el algoritmo AES<br /><br /> **Nota:** el algoritmo RC4 se admite únicamente por compatibilidad con versiones anteriores. El material nuevo solo se puede cifrar con RC4 o RC4_128 cuando la base de datos tenga el nivel de compatibilidad 90 o 100. (No se recomienda). Use un algoritmo más reciente como uno de los algoritmos AES en su lugar. En [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y versiones posteriores, el material cifrado con RC4 o RC4_128 se puede descifrar en cualquier nivel de compatibilidad.|  
|**encryption_algorithm_desc**|**nvarchar(60)**|Representación de texto del algoritmo de cifrado. ACEPTA VALORES NULL. Valores posibles:<br /><br /> **Descripción &#124; opción DDL correspondiente**<br /><br /> Ninguno &#124; deshabilitado<br /><br /> RC4 &#124; {necesario &#124; requiere el algoritmo RC4}<br /><br /> AES &#124; requiere el algoritmo AES<br /><br /> NONE, RC4 &#124; {admite &#124; admite el algoritmo RC4}<br /><br /> Ninguno, AES &#124; admite el algoritmo RC4<br /><br /> RC4, AES &#124; requiere el algoritmo RC4 AES<br /><br /> AES, RC4 &#124; requiere el algoritmo AES RC4<br /><br /> NONE, RC4, AES &#124; admite el algoritmo RC4 AES<br /><br /> Ninguno, AES, RC4 &#124; admite el algoritmo AES RC4|  
|**receives_posted**|**smallint**|Número de recepciones asincrónicas de red que aún no se han completado para esta conexión. ACEPTA VALORES NULL.|  
|**is_receive_flow_controlled**|**bit**|Determina si se han postergado las recepciones de red debido al control de flujo de la red porque la red está ocupada. ACEPTA VALORES NULL.<br /><br /> 1 = True|  
|**sends_posted**|**smallint**|El número de envíos asincrónicos de red que aún no se han completado para esta conexión. ACEPTA VALORES NULL.|  
|**is_send_flow_controlled**|**bit**|Determina si se han postergado los envíos de red debido al control de flujo de la red porque la red está ocupada. ACEPTA VALORES NULL.<br /><br /> 1 = True|  
|**total_bytes_sent**|**bigint**|Número total de bytes enviados por esta conexión. ACEPTA VALORES NULL.|  
|**total_bytes_received**|**bigint**|Número total de bytes recibidos por esta conexión. ACEPTA VALORES NULL.|  
|**total_fragments_sent**|**bigint**|Número total de fragmentos de mensaje de [!INCLUDE[ssSB](../../includes/sssb-md.md)] enviados por esta conexión. ACEPTA VALORES NULL.|  
|**total_fragments_received**|**bigint**|Número total de fragmentos de mensaje de [!INCLUDE[ssSB](../../includes/sssb-md.md)] recibidos por esta conexión. ACEPTA VALORES NULL.|  
|**total_sends**|**bigint**|Número total de solicitudes de envío de red emitidas por esta conexión. ACEPTA VALORES NULL.|  
|**total_receives**|**bigint**|Número total de red recibir solicitudes que hayan sido emitidas por esta conexión. ACEPTA VALORES NULL.|  
|**peer_arbitration_id**|**uniqueidentifier**|Identificador interno para el extremo. ACEPTA VALORES NULL.|  
  
## <a name="permissions"></a>Permissions  
 es necesario contar con el permiso VIEW SERVER STATE en el servidor.  
  
## <a name="physical-joins"></a>Combinaciones físicas  
 ![Combinaciones de sys.dm_broker_connections](../../relational-databases/system-dynamic-management-views/media/join-dm-broker-connections-1.gif "combinaciones de sys.dm_broker_connections")  
  
## <a name="relationship-cardinalities"></a>Cardinalidades de relación  
  
|De|En|Relación|  
|----------|--------|------------------|  
|**dm_broker_connections.connection_id**|**dm_exec_connections.connection_id**|Uno a uno|  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Service Broker relacionadas con vistas de administración dinámica & #40; Transact-SQL & #41;](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)  
  
  

