---
description: sys.soap_endpoints (Transact-SQL)
title: Sys. soap_endpoints (Transact-SQL) | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 051af6e1baa05698f7bc86c63a72c5e0cd6b1f0c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88475272"
---
# <a name="syssoap_endpoints-transact-sql"></a>sys.soap_endpoints (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 Contiene una fila para cada extremo del servidor que lleva una carga de tipo SOAP. Para cada fila de esta vista, hay una fila correspondiente con el mismo **endpoint_id** en la vista de catálogo **Sys. http_endpoints** que incluye los metadatos de configuración http.  
  
 
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**< columnas heredadas>**||Para obtener una lista de las columnas que hereda esta vista, vea [Sys. endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md).|  
|**is_sql_language_enabled**|**bit**|1 = Se ha especificado la opción BATCHES = ENABLED, es decir, que se permiten los lotes SQL ad hoc en el extremo.|  
|**wsdl_generator_procedure**|**nvarchar(776**|El nombre en tres partes del procedimiento almacenado que implementa este método.<br /><br /> Los nombres de métodos necesitan una sintaxis estricta de tres partes. No se permiten nombres de una, dos o cuatro partes.|  
|**default_database**|**sysname**|El nombre de la base de datos predeterminada proporcionado en la opción DATABASE =.<br /><br /> Se ha especificado NULL = DEFAULT.|  
|**default_namespace**|**nvarchar (384)**|El espacio de nombres predeterminado especificado en la opción NAMESPACE =, o `https://tempuri.org` si se ha especificado default en su lugar.|  
|**default_result_schema**|**tinyint**|El valor predeterminado de la opción SCHEMA =.<br /><br /> 0 = NONE<br /><br /> 1 = STANDARD|  
|**default_result_schema_desc**|**nvarchar(60)**|Descripción del valor predeterminado de la opción SCHEMA =.<br /><br /> Ninguno<br /><br /> STANDARD|  
|**is_xml_charset_enforced**|**bit**|0 = Se ha especificado la opción CHARACTER_SET = SQL.<br /><br /> 1 = Se ha especificado la opción CHARACTER_SET = XML.|  
|**is_session_enabled**|**bit**|0 = Se ha especificado la opción SESSION = DISABLE.<br /><br /> 1 = Se ha especificado la opción SESSION = ENABLED.|  
|**session_timeout**|**int**|Valor especificado en la opción SESSION_TIMEOUT =.|  
|**login_type**|**nvarchar(60)**|Tipo de autenticación permitido en este extremo.<br /><br /> WINDOWS<br /><br /> MIXED|  
|**header_limit**|**int**|Tamaño máximo permitido del encabezado SOAP.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte también  
 [Endpoints Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)  [Vistas de catálogo de extremos &#40;Transact-SQL&#41;]  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
