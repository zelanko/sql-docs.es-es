---
title: Sys.endpoint_webmethods (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
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
- sys.endpoint_webmethods_TSQL
- sys.endpoint_webmethods
- endpoint_webmethods_TSQL
- sys.http_soap_methods_TSQL
- endpoint_webmethods
- sys.http_soap_methods
dev_langs:
- TSQL
helpviewer_keywords:
- sys.endpoint_webmethods catalog view
ms.assetid: 7dad0cf6-eafa-47cf-98cc-75ba8d3c7959
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 93053b36893b6812128d2bb397a656d395f839af
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2017
---
# <a name="sysendpointwebmethods-transact-sql"></a>sys.endpoint_webmethods (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 Contiene una fila para cada método SOAP definido en un extremo HTTP habilitado por SOAP. La combinación de las columnas endpoint_id y espacio de nombres es única.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|endpoint_id|**int**|Identificador del extremo en el que está definido WEBMETHOD.|  
|espacio de nombres|**nvarchar (384)**|Espacio de nombres para WEBMETHOD.|  
|method_alias|**nvarchar(64)**|Alias del método.<br /><br /> Nota: [!INCLUDE[tsql](../../includes/tsql-md.md)] identificadores permiten caracteres que no son válidos en nombres de método WSDL.<br /><br /> El alias se utiliza para asignar el nombre expuesto en la descripción WSDL del extremo al objeto ejecutable de [!INCLUDE[tsql](../../includes/tsql-md.md)] subyacente real que se llama al invocar WEBMETHOD.|  
|object_name|**nvarchar(776)**|Nombre de objeto al que se redirige WEBMETHOD, como se especifica en la opción NAME =. Partes del nombre se separan con un punto (.) y se delimitan mediante corchetes, `[``]`.<br /><br /> El nombre de objeto debe constar de tres partes, como se especifica en la opción WSDL.|  
|result_schema|**tinyint**|Opción que determina si, en su caso, XSD se devuelve con una respuesta.<br /><br /> 0 = Ninguno<br /><br /> 1 = Estándar<br /><br /> 2 = Predeterminado|  
|result_schema_desc|**nvarchar (60)**|Descripción de opción que determina si, en su caso, XSD se devuelve con una respuesta.<br /><br /> Ninguno<br /><br /> STANDARD<br /><br /> DEFAULT|  
|result_format|**tinyint**|Opción que determina el formato que reciben los resultados en la respuesta.<br /><br /> 1 = ALL_RESULTS<br /><br /> 2 = ROWSETS_ONLY<br /><br /> 3 = NINGUNO|  
|result_format_desc|**nvarchar (60)**|Descripción de la opción que determina el formato que reciben los resultados en la respuesta.<br /><br /> ALL_RESULTS<br /><br /> ROWSETS_ONLY<br /><br /> Ninguno|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo de puntos de conexión &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/endpoints-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
