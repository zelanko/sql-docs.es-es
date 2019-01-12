---
title: CHECK_CONSTRAINTS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- CHECK_CONSTRAINTS
- CHECK_CONSTRAINTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CHECK_CONSTRAINTS view
- INFORMATION_SCHEMA.CHECK_CONSTRAINTS view
ms.assetid: e9577fd2-c349-4dff-874c-9e57d2e5a3ec
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 208950c30d11134c9d25a6b5be5f00abbc667558
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2019
ms.locfileid: "54131845"
---
# <a name="checkconstraints-transact-sql"></a>CHECK_CONSTRAINTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve una fila por cada restricción CHECK de la base de datos actual. Esta vista de esquema de información devuelve información acerca de los objetos para los que el usuario actual tiene permisos.  
  
 Para recuperar información de estas vistas, especifique el nombre completo de **INFORMATION_SCHEMA.** _view_name_.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**CONSTRAINT_CATALOG**|**nvarchar (** 128 **)**|Calificador de la restricción.|  
|**CONSTRAINT_SCHEMA**|**nvarchar (** 128 **)**|Nombre del esquema al que pertenece la restricción.<br /><br /> **&#42;&#42;Importante &#42; &#42;**  no utilice las vistas INFORMATION_SCHEMA para determinar el esquema de un objeto. La única manera confiable de localizar el esquema de un objeto consiste en consultar la vista de catálogo sys.objects.|  
|**CONSTRAINT_NAME**|**sysname**|Nombre de la restricción.|  
|**CHECK_CLAUSE**|**nvarchar (** 4000 **)**|Texto real de la instrucción de definición [!INCLUDE[tsql](../../includes/tsql-md.md)].|  
  
## <a name="see-also"></a>Vea también  
 [Vistas del sistema &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Vistas de esquema de información &#40;Transact-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [Sys.check_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
  
