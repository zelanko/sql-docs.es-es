---
title: VISTAS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- VIEWS_TSQL
- VIEWS
dev_langs:
- TSQL
helpviewer_keywords:
- VIEWS view
- INFORMATION_SCHEMA.VIEWS view
ms.assetid: 6119bc94-0b22-45d4-a34b-967afd810a9d
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 56ed627383b8ac80568b857d10e9d065a2bf9726
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51670014"
---
# <a name="views-transact-sql"></a>VIEWS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve una fila para las vistas a las que puede tener acceso el usuario actual en la base de datos actual.  
  
 Para recuperar información de estas vistas, especifique el nombre completo de **INFORMATION_SCHEMA. *** view_name*.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG**|**nvarchar (** 128 **)**|Calificador de la vista.|  
|**TABLE_SCHEMA**|**nvarchar (** 128 **)**|Nombre del esquema que contiene la vista.<br /><br /> **\*\* Importante \* \***  no utilice las vistas INFORMATION_SCHEMA para determinar el esquema de un objeto. La única manera confiable de localizar el esquema de un objeto consiste en consultar la vista de catálogo sys.objects.|  
|**TABLE_NAME**|**nvarchar (** 128 **)**|Nombre de la vista.|  
|**VIEW_DEFINITION**|**nvarchar (** 4000 **)**|Si es mayor que la longitud de la definición **nvarchar (** 4000 **)**, esta columna es NULL. De lo contrario, esta columna es el texto de la definición de la vista.|  
|**CHECK_OPTION**|**varchar (** 7 **)**|Tipo de WITH CHECK OPTION. Es CASCADE si la vista original se creó con WITH CHECK OPTION. En caso contrario se devuelve NONE.|  
|**IS_UPDATABLE**|**varchar (** 2 **)**|Especifica si la vista se puede actualizar. Siempre devuelve NO.|  
  
## <a name="see-also"></a>Vea también  
 [Vistas del sistema &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Vistas de esquema de información &#40;Transact-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-views-transact-sql.md)  
  
  
