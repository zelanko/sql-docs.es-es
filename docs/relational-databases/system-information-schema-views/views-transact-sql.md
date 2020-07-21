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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9aca4edc4d2b30eba8fe37467698f80b0c4ab5f4
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86006191"
---
# <a name="views-transact-sql"></a>VIEWS (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Devuelve una fila para las vistas a las que puede tener acceso el usuario actual en la base de datos actual.  
  
 Para recuperar información de estas vistas, especifique el nombre completo de **INFORMATION_SCHEMA.** _view_name_.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG**|**nvarchar (** 128 **)**|Calificador de la vista.|  
|**TABLE_SCHEMA**|**nvarchar (** 128 **)**|Nombre del esquema que contiene la vista.<br /><br /> **&#42;&#42; importante &#42;&#42;** única manera confiable de encontrar el esquema de un objeto consiste en consultar la vista de catálogo sys. Objects.|  
|**TABLE_NAME**|**nvarchar (** 128 **)**|Nombre de la vista.|  
|**VIEW_DEFINITION**|**nvarchar (** 4000 **)**|Si la longitud de la definición es mayor que **nvarchar (** 4000 **)**, esta columna es NULL. De lo contrario, esta columna es el texto de la definición de la vista.|  
|**CHECK_OPTION**|**VARCHAR (** 7 **)**|Tipo de WITH CHECK OPTION. Es CASCADE si la vista original se creó con WITH CHECK OPTION. En caso contrario se devuelve NONE.|  
|**IS_UPDATABLE**|**VARCHAR (** 2 **)**|Especifica si la vista se puede actualizar. Siempre devuelve NO.|  
  
## <a name="see-also"></a>Consulte también  
 [Vistas del sistema &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Vistas de esquema de información &#40;Transact-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [sys.views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-views-transact-sql.md)  
  
  
