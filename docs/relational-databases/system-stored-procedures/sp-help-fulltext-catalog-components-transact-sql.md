---
title: sp_help_fulltext_catalog_components (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_catalog_components_TSQL
- sp_help_fulltext_catalog_components
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_catalog_components
ms.assetid: fbd6a3d4-6a4c-42a2-bff8-2a5eb0745e47
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 687a624eea351433407ee88298a6520ceb213841
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82827716"
---
# <a name="sp_help_fulltext_catalog_components-transact-sql"></a>sp_help_fulltext_catalog_components (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una lista con todos los componentes (filtros, separadores de palabras y controladores de protocolo) que se usan en los catálogos de texto completo de la base de datos actual.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_help_fulltext_catalog_components  
```  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**nombre del catálogo de texto completo**|**int**|Nombre del catálogo de texto completo.|  
|**identificador del catálogo de texto completo**|**sysname**|Id. del catálogo de texto completo.|  
|**componenttype**|**sysname**|Tipo de componente. Uno de los siguientes:<br /><br /> Filtrar<br /><br /> Controlador de protocolo<br /><br /> Separador de palabras|  
|**componentName**|**sysname**|Nombre del componente.|  
|**CLSID**|**uniqueidentifier**|Identificador de clase del componente.|  
|**FullPath**|**nvarchar(256)**|Ruta de acceso a la ubicación del componente.<br /><br /> NULL = el autor de la llamada no es miembro del rol fijo de servidor **ServerAdmin** .|  
|**version**|**nvarchar(30)**|Versión del componente.|  
|**le**|**sysname**|Nombre del fabricante del componente.|  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol **public** .  
  
## <a name="see-also"></a>Consulte también  
 [Búsqueda de texto completo y procedimientos almacenados de búsqueda semántica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)   
 [Sys. fulltext_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)   
 [sp_help_fulltext_system_components &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md)   
 [Búsqueda de texto completo](../../relational-databases/search/full-text-search.md)  
  
  
