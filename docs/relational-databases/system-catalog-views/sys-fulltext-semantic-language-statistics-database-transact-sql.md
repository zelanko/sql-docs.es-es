---
title: Sys.fulltext_semantic_language_statistics_database (Transact-SQL) | Documentos de Microsoft
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
- sys.fulltext_semantic_language_statistics_database_TSQL
- fulltext_semantic_language_statistics_database_TSQL
- fulltext_semantic_language_statistics_database
- sys.fulltext_semantic_language_statistics_database
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_semantic_language_statistics_database catalog view
ms.assetid: 32e95614-ed88-4068-8c37-1e21544717bc
caps.latest.revision: 14
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e5e84ee0b65a38766f7d6a58e0488cb98c1b7a99
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="sysfulltextsemanticlanguagestatisticsdatabase-transact-sql"></a>sys.fulltext_semantic_language_statistics_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila sobre la base de datos de estadísticas semánticas de lenguaje instalada en la instancia actual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Puede consultar esta vista para encontrar el componente de estadísticas semánticas de lenguaje necesario para el procesamiento semántico.  
   
  
||||  
|-|-|-|  
|**Nombre de columna**|**Tipo**|**Description**|  
|**database_id**|**int**|Id. de la base de datos, único en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**register_date**|**datetime**|Fecha en que la base de datos se registró para el procesamiento semántico.|  
|**registered_by**|**int**|Identificador de la entidad de seguridad de servidor que registró la base de datos para el procesamiento semántico.|  
|**version**|**nvarchar(128)**|La última información de versión específica de la base de datos de estadísticas semánticas de lenguaje.|  
  
## <a name="general-remarks"></a>Notas generales  
 Para obtener más información, vea [Instalar y configurar la búsqueda semántica](../../relational-databases/search/install-and-configure-semantic-search.md).  
  
## <a name="metadata"></a>Metadatos  
 Para obtener información acerca de los idiomas que se admiten para la indización semántica, consulte la vista de catálogo [sys.fulltext_semantic_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-semantic-languages-transact-sql.md).  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permissions  
 La visibilidad de los metadatos en las vistas de catálogo se limita a los elementos protegibles y que son propiedad de un usuario o sobre los que el usuario tiene algún permiso.  
  
## <a name="examples"></a>Ejemplos  
 El siguiente ejemplo se muestra cómo consultar **sys.fulltext_semantic_language_statistics_database** para obtener información acerca de la base de datos de estadísticas semánticas de lenguaje registrado en la instancia actual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
SELECT * FROM sys.fulltext_semantic_language_statistics_database;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Instalar y configurar la búsqueda semántica](../../relational-databases/search/install-and-configure-semantic-search.md)  
  
  
