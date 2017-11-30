---
title: Sys.xml_schema_components (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- xml_schema_components
- sys.xml_schema_components_TSQL
- sys.xml_schema_components
- xml_schema_components_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.xml_schema_components catalog view
ms.assetid: 70142d3a-f8b5-4ee2-8287-3935f0f67aa2
caps.latest.revision: "35"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7a3e5b71a36df056dbba198a86af316d32fb9eaf
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2017
---
# <a name="sysxmlschemacomponents-transact-sql"></a>sys.xml_schema_components (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila por componente de un esquema XML. El par (**collection_id**, **namespace_id**) es una clave externa compuesta para el espacio de nombres contenedor. Para los componentes con nombre, los valores de **symbol_space**, **nombre**, **scoping_xml_component_id**, **is_qualified**,  **xml_namespace_id**, **xml_collection_id** son únicos.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**xml_component_id**|**int**|Id. único del componente del esquema XML en la base de datos.|  
|**xml_collection_id**|**int**|Id. de la colección de esquemas XML que contiene el espacio de nombres de este componente.|  
|**xml_namespace_id**|**int**|Id. del espacio de nombres XML en la colección.|  
|**is_qualified**|**bit**|1 = Este componente tiene un espacio de nombres calificado explícito.<br /><br /> 0 = Es un componente de ámbito local. En este caso, el par **namespace_id**, **collection_id**, hace referencia a la "ningún espacio de nombres" **targetNamespace**.<br /><br /> Para componentes comodín, este valor será 1.|  
|**Nombre**|**nvarchar**<br /><br /> **(4000)**|Nombre único del componente del esquema XML. Es NULL si el componente no tiene nombre.|  
|**symbol_space**|**Char (1)**|Espacio en el que este nombre simbólico es único, en función de **tipo**:<br /><br /> N = Ninguno<br /><br /> T = Tipo<br /><br /> E = Elemento<br /><br /> M = Grupo de modelos<br /><br /> A = Atributo<br /><br /> G = Grupo de atributos|  
|**symbol_space_desc**|**nvarchar**<br /><br /> **(60)**|Descripción del espacio en el que este nombre simbólico es único, en función de **tipo**:<br /><br /> Ninguno<br /><br /> TYPE<br /><br /> ELEMENT<br /><br /> MODEL_GROUP<br /><br /> ATTRIBUTE<br /><br /> ATTRIBUTE_GROUP|  
|**tipo**|**Char (1)**|Tipo del componente del esquema XML.<br /><br /> N = Cualquier tipo (componente intrínseco especial)<br /><br /> Z = Cualquier tipo simple (componente intrínseco especial)<br /><br /> P = Tipo primitivo (tipos intrínsecos)<br /><br /> S = Tipo simple<br /><br /> L = Tipo de lista<br /><br /> U = Tipo de unión<br /><br /> C = Tipo simple complejo (derivado de simple)<br /><br /> K = Tipo complejo<br /><br /> E = Elemento<br /><br /> M = Grupo de modelos<br /><br /> W = Comodín de elementos<br /><br /> A = Atributo<br /><br /> G = Grupo de atributos<br /><br /> V = Comodín de atributos|  
|**kind_desc**|**nvarchar**<br /><br /> **(60)**|Descripción del tipo de componente del esquema XML.<br /><br /> ANY_TYPE<br /><br /> ANY_SIMPLE_TYPE<br /><br /> PRIMITIVE_TYPE<br /><br /> SIMPLE_TYPE<br /><br /> LIST_TYPE<br /><br /> UNION_TYPE<br /><br /> COMPLEX_SIMPLE_TYPE<br /><br /> COMPLEX_TYPE<br /><br /> ELEMENT<br /><br /> MODEL_GROUP<br /><br /> ELEMENT_WILDCARD<br /><br /> ATTRIBUTE<br /><br /> ATTRIBUTE_GROUP<br /><br /> ATTRIBUTE_WILDCARD|  
|**derivación**|**Char (1)**|Método de derivación para tipos derivados:<br /><br /> N = Ninguno (no derivado)<br /><br /> X = Extensión<br /><br /> R = Restricción<br /><br /> S = Sustitución|  
|**derivation_desc**|**nvarchar**<br /><br /> **(60)**|Descripción del método de derivación para tipos derivados:<br /><br /> Ninguno<br /><br /> EXTENSION<br /><br /> RESTRICTION<br /><br /> SUBSTITUTION|  
|**base_xml_component_id**|**int**|Id. del componente del que se deriva este componente. Es NULL si no hay ninguno.|  
|**scoping_xml_component_id**|**int**|Id. único del componente de alcance. Es NULL si no hay ninguno (espacio global).|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Esquemas XML &#40; Sistema de tipo XML &#41; Vistas de catálogo &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/xml-schemas-xml-type-system-catalog-views-transact-sql.md)  
  
  
