---
title: Sys.http_endpoints (Transact-SQL) | Documentos de Microsoft
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
- sys.http_endpoints
- http_endpoints
- sys.http_endpoints_TSQL
- http_endpoints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.http_endpoints catalog view
ms.assetid: 16f59695-ecd9-457e-8874-055af63f8ea7
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: b0bd82aa39d7639c52c7c18c35091adc18b4b485
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33180781"
---
# <a name="syshttpendpoints-transact-sql"></a>sys.http_endpoints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila para cada extremo creado en el servidor que utiliza el protocolo HTTP.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**< columnas heredadas >**||Hereda columnas de [sys.endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-endpoints-transact-sql.md).|  
|**Sitio**|**nvarchar(128)**|Nombre del equipo host del sitio según se especifica en la opción SITE =.|  
|**url_path**|**nvarchar(4000)**|Parte solo de la ruta de la URL para este extremo HTTP según se especifica en la opción PATH=.|  
|**is_clear_port_enabled**|**bit**|1 = Puerto libre habilitado con la opción PORT = CLEAR.|  
|**CLEAR_PORT**|**int**|Número de puerto especificado con la opción CLEAR PORT =.<br /><br /> NULL = Sin especificar.|  
|**is_ssl_port_enabled**|**bit**|1 = Puerto SSL habilitado con la opción PORT = SSL.|  
|**SSL_PORT**|**int**|Número de puerto especificado con la opción SSL PORT =.<br /><br /> NULL = Sin especificar.|  
|**is_anonymous_enabled**|**bit**|1 = Acceso anónimo habilitado con la opción AUTHENTICATION = ANONYMOUS.|  
|**is_basic_auth_enabled**|**bit**|1 = Autenticación básica habilitada con la opción AUTHENTICATION = BASIC.|  
|**is_digest_auth_enabled**|**bit**|1 = Autenticación implícita habilitada con la opción AUTHENTICATION = DIGEST.|  
|**is_kerberos_auth_enabled**|**bit**|1 = Autenticación integrada habilitada con la opción AUTHENTICATION = KERBEROS.|  
|**is_ntlm_auth_enabled**|**bit**|1 = Autenticación integrada habilitada con la opción AUTHENTICATION = NTLM.|  
|**is_integrated_auth_enabled**|**bit**|1 = Autenticación integrada habilitada con la opción AUTHENTICATION = INTEGRATED.|  
|**authorization_realm**|**nvarchar(128)**|Sugerencia devuelta al cliente como parte del desafío de la autenticación HTTP DIGEST. Es el valor de la opción AUTH REALM.<br /><br /> Es NULL si no se especifica o si la autenticación DIGEST no está habilitada.|  
|**DEFAULT_LOGON_DOMAIN**|**nvarchar(128)**|Dominio de inicio de sesión predeterminado al habilitar la autenticación BASIC. Es el valor de la opción DEFAULT LOGON DOMAIN.<br /><br /> Es NULL si no se especifica o si la autenticación BASIC no está habilitada.|  
|**is_compression_enabled**|**bit**|1 = Se establece la opción COMPRESSION = ENABLED.|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Vistas de catálogo de extremos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)  
  
  
