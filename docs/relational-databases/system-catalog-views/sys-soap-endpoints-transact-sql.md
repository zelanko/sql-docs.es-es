---
title: Sys.soap_endpoints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 251e5f79c03c02499aec9f3c0f90f42902d32474
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51656614"
---
# <a name="syssoapendpoints-transact-sql"></a>sys.soap_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 Contiene una fila para cada extremo del servidor que lleva una carga de tipo SOAP. Para cada fila de esta vista, hay una fila correspondiente con el mismo **endpoint_id** en el **sys.http_endpoints** vista de catálogo que incluye los metadatos de configuración de HTTP.  
  
 
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**< columnas heredadas >**||Para obtener una lista de columnas que hereda esta vista, consulte [sys.endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md).|  
|**is_sql_language_enabled**|**bit**|1 = Se ha especificado la opción BATCHES = ENABLED, es decir, que se permiten los lotes SQL ad hoc en el extremo.|  
|**wsdl_generator_procedure**|**nvarchar(776)**|El nombre en tres partes del procedimiento almacenado que implementa este método.<br /><br /> Los nombres de métodos necesitan una sintaxis estricta de tres partes. No se permiten nombres de una, dos o cuatro partes.|  
|**default_database**|**sysname**|El nombre de la base de datos predeterminada proporcionado en la opción DATABASE =.<br /><br /> Se ha especificado NULL = DEFAULT.|  
|**default_namespace**|**nvarchar(384)**|El espacio de nombres predeterminado especificado en el espacio de nombres = opción, o `https://tempuri.org` si se ha especificado DEFAULT en su lugar.|  
|**default_result_schema**|**tinyint**|El valor predeterminado de la opción SCHEMA =.<br /><br /> 0 = NONE<br /><br /> 1 = STANDARD|  
|**default_result_schema_desc**|**nvarchar(60)**|Descripción del valor predeterminado de la opción SCHEMA =.<br /><br /> Ninguno<br /><br /> STANDARD|  
|**is_xml_charset_enforced**|**bit**|0 = Se ha especificado la opción CHARACTER_SET = SQL.<br /><br /> 1 = Se ha especificado la opción CHARACTER_SET = XML.|  
|**is_session_enabled**|**bit**|0 = Se ha especificado la opción SESSION = DISABLE.<br /><br /> 1 = Se ha especificado la opción SESSION = ENABLED.|  
|**session_timeout**|**int**|Valor especificado en la opción SESSION_TIMEOUT =.|  
|**login_type**|**nvarchar(60)**|Tipo de autenticación permitido en este extremo.<br /><br /> WINDOWS<br /><br /> MIXED|  
|**HEADER_LIMIT**|**int**|Tamaño máximo permitido del encabezado SOAP.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Endpoints Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)  [Vistas de catálogo de extremos &#40;Transact-SQL&#41;]  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
