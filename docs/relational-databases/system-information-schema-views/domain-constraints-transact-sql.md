---
title: DOMAIN_CONSTRAINTS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DOMAIN_CONSTRAINTS
- DOMAIN_CONSTRAINTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.DOMAIN_CONSTRAINTS view
- DOMAIN_CONSTRAINTS view
ms.assetid: 436c4480-f1e3-403f-b2bd-de04539afe3c
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7b8935bc203c616f88a7e5929bd19e10a41592d3
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/18/2018
ms.locfileid: "53591039"
---
# <a name="domainconstraints-transact-sql"></a>DOMAIN_CONSTRAINTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve una fila por cada tipo de datos de alias de la base de datos actual que tenga una regla enlazada y a la que el usuario actual puede tener acceso.  
  
 Para recuperar información de estas vistas, especifique el nombre completo de **INFORMATION_SCHEMA.** _view_name_.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**CONSTRAINT_CATALOG**|**nvarchar (** 128 **)**|Base de datos en la que existe la regla.|  
|**CONSTRAINT_SCHEMA**|**nvarchar (** 128 **)**|Nombre del esquema que contiene la restricción.<br /><br /> <strong>\*\* Importante \* \*</strong>  no utilice las vistas INFORMATION_SCHEMA para determinar el esquema de un objeto. La única manera confiable de localizar el esquema de un objeto consiste en consultar la vista de catálogo sys.objects.|  
|**CONSTRAINT_NAME**|**sysname**|Nombre de la regla.|  
|**DOMAIN_CATALOG**|**nvarchar (** 128 **)**|Base de datos donde existe el tipo de datos de alias.|  
|**DOMAIN_SCHEMA**|**nvarchar (** 128 **)**|Nombre del esquema que contiene el tipo de datos de alias.<br /><br /> <strong>\*\* Importante \* \*</strong>  no utilice las vistas INFORMATION_SCHEMA para determinar el esquema de un tipo de datos. La única manera confiable de localizar el esquema de un tipo consiste en utilizar la función TYPEPROPERTY.|  
|**NOMBRE_DOMINIO**|**sysname**|Tipo de datos de alias.|  
|**IS_DEFERRABLE**|**varchar (** 2 **)**|Especifica si la comprobación de la restricción se puede aplazar. Siempre devuelve NO.|  
|**INITIALLY_DEFERRED**|**varchar (** 2 **)**|Especifica si la comprobación de la restricción se aplaza inicialmente. Siempre devuelve NO.|  
  
## <a name="see-also"></a>Vea también  
 [Vistas del sistema &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Vistas de esquema de información &#40;Transact-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)  
  
  
