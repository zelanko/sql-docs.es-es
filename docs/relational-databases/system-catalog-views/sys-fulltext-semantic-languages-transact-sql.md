---
title: Sys. fulltext_semantic_languages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fulltext_semantic_languages
- fulltext_semantic_languages_TSQL
- sys.fulltext_semantic_languages
- sys.fulltext_semantic_languages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fulltext_semantic_languages catalog view
ms.assetid: b42a85e6-1db9-4a22-8a70-014574c95198
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
ms.openlocfilehash: a345e41f42cc70e941e4a87e3510312313d4dc03
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85764665"
---
# <a name="sysfulltext_semantic_languages-transact-sql"></a>sys.fulltext_semantic_languages (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Devuelve una fila por cada idioma cuyo modelo de estadísticas se registra con la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Cuando se registra un modelo de idioma, el idioma se habilita para la indización semántica.  
  
 Esta vista de catálogo es similar a [Sys. fulltext_languages &#40;&#41;de Transact-SQL ](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md).  
    
||||  
|-|-|-|  
|**Nombre de la columna**|**Type**|**Descripción**|  
|lcid|int|Identificador de configuración regional (LCID) de Microsoft Windows para el idioma.|  
|name|sysname|Es el valor del alias en [sys.syslenguajes &#40;&#41;de Transact-SQL](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) que corresponde al valor de **LCID**o la representación de cadena del LCID numérico.|  
  
## <a name="general-remarks"></a>Notas generales  
 Para obtener más información, vea [Instalar y configurar la búsqueda semántica](../../relational-databases/search/install-and-configure-semantic-search.md).  
  
## <a name="metadata"></a>Metadatos  
 Para obtener más información acerca de la base de datos de estadísticas semánticas de lenguaje que se instala para admitir la indización semántica, consulte la vista de catálogo [Sys. fulltext_semantic_language_statistics_database &#40;&#41;de Transact-SQL ](../../relational-databases/system-catalog-views/sys-fulltext-semantic-language-statistics-database-transact-sql.md).  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permisos  
 La visibilidad de los metadatos en las vistas de catálogo se limita a los elementos protegibles y que son propiedad de un usuario o sobre los que el usuario tiene algún permiso.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra cómo consultar **Sys. fulltext_semantic_languages** para obtener información sobre todos los modelos de lenguaje registrados para la indización semántica en la instancia actual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
```  
SELECT * FROM sys.fulltext_semantic_languages;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [Instalar y configurar la búsqueda semántica](../../relational-databases/search/install-and-configure-semantic-search.md)  
  
  
