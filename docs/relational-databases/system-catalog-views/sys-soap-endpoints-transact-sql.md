---
title: Sys.soap_endpoints (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- soap_endpoints_TSQL
- sys.soap_endpoints
- soap_endpoints
- sys.soap_endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.soap_endpoints catalog view
ms.assetid: f50dcbfc-02ed-4a19-9c07-c78a5a1b3224
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 38bc05ab3d49716f2c4fc484098c4ff838bc634e
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="syssoapendpoints-transact-sql"></a>sys.soap_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 Contiene una fila para cada extremo del servidor que lleva una carga de tipo SOAP. Para cada fila de esta vista, no hay una fila correspondiente con el mismo **endpoint_id** en el **sys.http_endpoints** vista de catálogo que contiene los metadatos de configuración de HTTP.  
  
 
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**< columnas heredadas >**||Para obtener una lista de columnas que hereda esta vista, consulte [sys.endpoints &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md).|  
|**is_sql_language_enabled**|**bit**|1 = Se ha especificado la opción BATCHES = ENABLED, es decir, que se permiten los lotes SQL ad hoc en el extremo.|  
|**wsdl_generator_procedure**|**nvarchar(776)**|El nombre en tres partes del procedimiento almacenado que implementa este método.<br /><br /> Los nombres de métodos necesitan una sintaxis estricta de tres partes. No se permiten nombres de una, dos o cuatro partes.|  
|**DEFAULT_DATABASE**|**sysname**|El nombre de la base de datos predeterminada proporcionado en la opción DATABASE =.<br /><br /> Se ha especificado NULL = DEFAULT.|  
|**default_namespace**|**nvarchar (384)**|El espacio de nombres especificado en la opción NAMESPACE =, o 'http://tempuri.org' si se ha especificado DEFAULT.|  
|**default_result_schema**|**tinyint**|El valor predeterminado de la opción SCHEMA =.<br /><br /> 0 = NONE<br /><br /> 1 = STANDARD|  
|**default_result_schema_desc**|**nvarchar (60)**|Descripción del valor predeterminado de la opción SCHEMA =.<br /><br /> Ninguno<br /><br /> STANDARD|  
|**is_xml_charset_enforced**|**bit**|0 = Se ha especificado la opción CHARACTER_SET = SQL.<br /><br /> 1 = Se ha especificado la opción CHARACTER_SET = XML.|  
|**is_session_enabled**|**bit**|0 = Se ha especificado la opción SESSION = DISABLE.<br /><br /> 1 = Se ha especificado la opción SESSION = ENABLED.|  
|**SESSION_TIMEOUT**|**int**|Valor especificado en la opción SESSION_TIMEOUT =.|  
|**LOGIN_TYPE**|**nvarchar (60)**|Tipo de autenticación permitido en este extremo.<br /><br /> WINDOWS<br /><br /> MIXED|  
|**HEADER_LIMIT**|**int**|Tamaño máximo permitido del encabezado SOAP.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo de puntos de conexión &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
