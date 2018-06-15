---
title: Sys.soap_endpoints (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 7f3af00bccbef87dd6390c5421b8d625e4b6ed42
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33221356"
---
# <a name="syssoapendpoints-transact-sql"></a>sys.soap_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 Contiene una fila para cada extremo del servidor que lleva una carga de tipo SOAP. Para cada fila de esta vista, no hay una fila correspondiente con el mismo **endpoint_id** en el **sys.http_endpoints** vista de catálogo que contiene los metadatos de configuración de HTTP.  
  
 
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**< columnas heredadas >**||Para obtener una lista de columnas que hereda esta vista, consulte [sys.endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md).|  
|**is_sql_language_enabled**|**bit**|1 = Se ha especificado la opción BATCHES = ENABLED, es decir, que se permiten los lotes SQL ad hoc en el extremo.|  
|**wsdl_generator_procedure**|**nvarchar(776)**|El nombre en tres partes del procedimiento almacenado que implementa este método.<br /><br /> Los nombres de métodos necesitan una sintaxis estricta de tres partes. No se permiten nombres de una, dos o cuatro partes.|  
|**default_database**|**sysname**|El nombre de la base de datos predeterminada proporcionado en la opción DATABASE =.<br /><br /> Se ha especificado NULL = DEFAULT.|  
|**default_namespace**|**nvarchar(384)**|El espacio de nombres predeterminado especificado en el espacio de nombres = opción, o 'http://tempuri.org' si se especifica DEFAULT en su lugar.|  
|**default_result_schema**|**tinyint**|El valor predeterminado de la opción SCHEMA =.<br /><br /> 0 = NONE<br /><br /> 1 = STANDARD|  
|**default_result_schema_desc**|**nvarchar(60)**|Descripción del valor predeterminado de la opción SCHEMA =.<br /><br /> Ninguno<br /><br /> STANDARD|  
|**is_xml_charset_enforced**|**bit**|0 = Se ha especificado la opción CHARACTER_SET = SQL.<br /><br /> 1 = Se ha especificado la opción CHARACTER_SET = XML.|  
|**is_session_enabled**|**bit**|0 = Se ha especificado la opción SESSION = DISABLE.<br /><br /> 1 = Se ha especificado la opción SESSION = ENABLED.|  
|**session_timeout**|**int**|Valor especificado en la opción SESSION_TIMEOUT =.|  
|**login_type**|**nvarchar(60)**|Tipo de autenticación permitido en este extremo.<br /><br /> WINDOWS<br /><br /> MIXED|  
|**HEADER_LIMIT**|**int**|Tamaño máximo permitido del encabezado SOAP.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Endpoints Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)  [Vistas de catálogo de extremos &#40;Transact-SQL&#41;]  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
