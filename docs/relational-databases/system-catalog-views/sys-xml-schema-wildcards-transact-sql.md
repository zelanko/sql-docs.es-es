---
title: sys.xml_schema_wildcards (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.xml_schema_wildcards
- sys.xml_schema_wildcards_TSQL
- xml_schema_wildcards
- xml_schema_wildcards_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_wildcards catalog view
ms.assetid: 7cedfe9a-e99e-4777-8a28-98674b6e5cff
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f4ff9c2c12dbbf930fd1f4d025ad96f79d089d4c
ms.sourcegitcommit: 04c031f7411aa33e2174be11dfced7feca8fbcda
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/30/2019
ms.locfileid: "64945800"
---
# <a name="sysxmlschemawildcards-transact-sql"></a>sys.xml_schema_wildcards (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila por cada componente del esquema XML que es un comodín de atributo (**tipo** de **V**) o comodín de elementos (**tipo** de **W**), ambos con **symbol_space** de **N**.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**\<hereda columnas >**||Hereda columnas de [sys.xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md).|  
|**process_content**|**char(1)**|Indica cómo se procesa el contenido.<br /><br /> S = Validación estricta (debe validarse)<br /><br /> L = Validación flexible (validar si es posible)<br /><br /> P = Omitir validación|  
|**process_content_desc**|**nvarchar(60)**|Descripción de cómo se procesa el contenido.<br /><br /> **STRICT_VALIDATION**<br /><br /> **LAX_VALIDATION**<br /><br /> **SKIP_VALIDATION**|  
|**disallow_namespaces**|**bit**|0 = los espacios de nombres enumerado en [sys.xml_schema_wildcard_namespaces](../../relational-databases/system-catalog-views/sys-xml-schema-wildcard-namespaces-transact-sql.md) son los únicos permitidos.<br /><br /> 1 = Los espacios de nombres son los únicos que no se permiten.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Los esquemas XML &#40;sistema de tipo XML&#41; vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
