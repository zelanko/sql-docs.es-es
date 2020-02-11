---
title: Sys. numbered_procedures (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.numbered_procedures_TSQL
- numbered_procedures
- sys.numbered_procedures
- numbered_procedures_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.numbered_procedures catalog view
ms.assetid: 5b6d6498-bac6-4266-94b9-d16ef5089cf0
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1d0fa4c5ef671d643f85fa2a1a2d0caa62d00d86
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68102301"
---
# <a name="sysnumbered_procedures-transact-sql"></a>sys.numbered_procedures (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Contiene una fila para cada procedimiento almacenado de SQL Server creado como procedimiento numerado. No se muestra una fila para el procedimiento almacenado base (número = 1). Las entradas de los procedimientos almacenados base se pueden encontrar en vistas como **Sys. Objects** y **Sys. Procedures**.  
  
> [!IMPORTANT]  
>  Los procedimientos numerados son desusados. Por tanto, se desaconseja su uso. Se desencadena un evento DEPRECATION_ANNOUNCEMENT cuando se compila una consulta que utiliza esta vista de catálogo.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|Id. del objeto del procedimiento almacenado.|  
|**procedure_number**|**smallint**|Número de este procedimiento en el objeto, 2 o mayor.|  
|**definir**|**nvarchar(max)**|Texto de SQL Server que define este procedimiento.<br /><br /> NULL = cifrado.|  
  
> [!NOTE]  
>  Los parámetros XML y CLR no son compatibles con los procedimientos numerados.  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo de objetos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
