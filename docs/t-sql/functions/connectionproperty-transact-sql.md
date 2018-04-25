---
title: CONNECTIONPROPERTY (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CONNECTIONPROPERTY_TSQL
- CONNECTIONPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- CONNECTIONPROPERTY statement
ms.assetid: 6bd9ccae-af77-4a05-b97f-f8ab41cfde42
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 95c95ad472c5b5d4cb5420fa3b0da8f88053c0c5
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="connectionproperty-transact-sql"></a>CONNECTIONPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve información acerca de las propiedades de conexión de la única conexión encontrada por una solicitud.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
CONNECTIONPROPERTY ( property )  
```  
  
## <a name="arguments"></a>Argumentos  
*property*  
Es la propiedad de la conexión. *property* puede tener uno de estos valores.
  
|Valor|Tipo de datos|Description|  
|---|---|---|
|net_transport|**nvarchar(40)**|Devuelve el protocolo de transporte físico utilizado por esta conexión. No admite valores NULL.<br /><br /> Los valores devueltos son: **HTTP**, **Named pipe**, **Session**, **Shared memory**, **SSL**, **TCP** y **VIA**.<br /><br /> Nota: Siempre se devuelve **Session** cuando una conexión tiene habilitado Multiple Active Result Sets (MARS) y la agrupación de conexiones está habilitada.|  
|protocol_type|**nvarchar(40)**|Devuelve el tipo de protocolo de la carga. Actualmente, distingue entre TDS (TSQL) y SOAP. Acepta valores NULL.|  
|auth_scheme|**nvarchar(40)**|Devuelve el esquema de autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de una conexión. El esquema de autenticación puede utilizar la autenticación de Windows (NTLM, KERBEROS, DIGEST, BASIC, NEGOTIATE) o la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. No admite valores NULL.|  
|local_net_address|**varchar(48)**|Devuelve la dirección IP del servidor que es el destino de esta conexión. Solo está disponible para las conexiones que utilicen el proveedor de transporte TCP. Acepta valores NULL.|  
|local_tcp_port|**int**|Devuelve el puerto TCP del servidor de destino de esta conexión, si se trata de una conexión que utiliza el transporte TCP. Acepta valores NULL.|  
|client_net_address|**varchar(48)**|Solicita la dirección del cliente que se está conectando a este servidor. Acepta valores NULL.|  
|physical_net_transport|**nvarchar(40)**|Devuelve el protocolo de transporte físico utilizado por esta conexión. Preciso cuando una conexión tiene habilitado Multiple Active Result Sets (MARS).|  
|\<Cualquier otra cadena>||Devuelve NULL si la entrada no es válida.|  
  
## <a name="remarks"></a>Notas  
**local_net_address** y **local_tcp_port** devuelven NULL en [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].
  
Los valores devueltos son iguales que las opciones mostradas en las columnas correspondientes de la vista de administración dinámica [sys.dm_exec_connections](../../relational-databases/system-dynamic-management-views/sys-dm-exec-connections-transact-sql.md). Por ejemplo:
  
```sql
SELECT   
ConnectionProperty('net_transport') AS 'Net transport',   
ConnectionProperty('protocol_type') AS 'Protocol type';  
```  
  
## <a name="see-also"></a>Vea también
[sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
[sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)
  
  
