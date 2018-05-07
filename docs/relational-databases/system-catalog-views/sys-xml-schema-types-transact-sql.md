---
title: Sys.xml_schema_types (Transact-SQL) | Documentos de Microsoft
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
- sys.xml_schema_types_TSQL
- xml_schema_types_TSQL
- sys.xml_schema_types
- xml_schema_types
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_schema_types catalog view
ms.assetid: 441ba49d-f778-4fa1-98c4-ced375a01a34
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: cf2399cea1d510eaba51119b01d66e2e44113fd0
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="sysxmlschematypes-transact-sql"></a>sys.xml_schema_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila por cada componente del esquema XML que es un tipo, **symbol_space** de **T**.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**\<hereda columnas >**||Hereda columnas de [sys.xml_schema_components](../../relational-databases/system-catalog-views/sys-xml-schema-components-transact-sql.md).|  
|**is_abstract**|**bit**|1 = El tipo es un tipo abstracto. Todas las instancias de un elemento de este tipo deben usar **xsi: Type** para indicar un tipo derivado que no es abstracto.<br /><br /> 0 = El tipo no es abstracto. (predeterminado).|  
|**allows_mixed_content**|**bit**|1 = Se permite contenido mixto<br /><br /> 0 = No se permite contenido mixto. (predeterminado).|  
|**is_extension_blocked**|**bit**|1 = el reemplazo con una extensión del tipo está bloqueado en instancias cuando el bloque de atributo en el **complexType** definición o el **blockDefault** atributo del antecesor \<esquema > información de elemento se establece en "extension" o "#all".<br /><br /> 0 = El reemplazo con una extensión no está bloqueado.|  
|**is_restriction_blocked**|**bit**|1 = el reemplazo con una restricción del tipo está bloqueado en instancias cuando el bloque de atributo en el **complexType** definición o el **blockDefault** atributo del antecesor \<esquema > información de elemento se establece en "restriction" o "#all".<br /><br /> 0 = El reemplazo con una restricción no está bloqueado. (predeterminado).|  
|**is_final_extension**|**bit**|1 = la derivación por extensión del tipo está bloqueada cuando el atributo final de la **complexType** definición o el **finalDefault** atributo del antecesor \<esquema > información de elemento elemento se establece en "extension" o "#all".<br /><br /> 0 = Se permite la extensión. (predeterminado).|  
|**is_final_restriction**|**bit**|1 = la derivación por restricción del tipo está bloqueada cuando el atributo final en simple o **complexType** definición o el **finalDefault** atributo del antecesor \<esquema > elemento elemento de información se establece en "restriction" o "#all".<br /><br /> 0 = Se permite la restricción. (predeterminado).|  
|**is_final_list_member**|**bit**|1 = Este tipo simple no se puede utilizar como tipo de elemento en una lista.<br /><br /> 0 = Este tipo es un tipo complejo o se puede utilizar como un tipo de elemento de lista. (predeterminado).|  
|**is_final_union_member**|**bit**|1 = Este tipo simple no se puede utilizar como tipo de miembro de un tipo de unión.<br /><br /> 0 = Este tipo es un tipo complejo. o se puede utilizar como tipo de miembro de unión. (predeterminado).|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Esquemas XML &#40;sistema de tipo XML&#41; vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
