---
title: Sys.systypes (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.systypes_TSQL
- systypes_TSQL
- sys.systypes
- systypes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.systypes compatibility view
- systypes system table
ms.assetid: 1b0b1d0c-5f7b-470b-bd52-8bfa922d7889
caps.latest.revision: 50
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: c0744091947e1a0c3a101b9c09dd242fc8bef30b
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="syssystypes-transact-sql"></a>sys.systypes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve una fila por cada tipo de datos que suministra el sistema o que define el usuario en la base de datos.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**Nombre**|**sysname**|Nombre del tipo de datos.|  
|**alguno**|**tinyint**|Tipo de almacenamiento físico.|  
|**status**|**tinyint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xusertype**|**smallint**|Tipo extendido de usuario. Produce un desbordamiento o devuelve NULL si el número de tipos de datos es superior a 32.767.|  
|**length**|**smallint**|Longitud física del tipo de datos.|  
|**xprec**|**tinyint**|Precisión interna que usa el servidor. No debe utilizarse en consultas.|  
|**XScale**|**tinyint**|Escala interna que usa el servidor. No debe utilizarse en consultas.|  
|**TNO**|**int**|Id. del procedimiento almacenado que contiene comprobaciones de integridad para este tipo de datos.|  
|**Dominio**|**int**|Id. del procedimiento almacenado que contiene comprobaciones de integridad para este tipo de datos.|  
|**UID**|**smallint**|Id. de esquema del propietario del tipo.<br /><br /> Para bases de datos actualizadas a partir de una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el identificador de esquema es igual que el identificador de usuario del propietario.<br /><br /> **\*\* Importante \* \***  si utiliza alguna de las siguientes acciones [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instrucciones DDL, debe utilizar el [sys.types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md) en lugar de la vista de catálogo **sys.systypes**.<br /><br /> ALTER AUTHORIZATION ON TYPE<br /><br /> CREATE TYPE<br /><br /> Produce un desbordamiento o devuelve NULL si el número de usuarios y roles es superior a 32.767.|  
|**Reservado**|**smallint**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**collationid**|**int**|Si se basa en caracteres, **collationid** es el identificador de la intercalación de la base de datos actual; en caso contrario, es NULL.|  
|**usertype**|**smallint**|Identificador de tipo de usuario. Produce un desbordamiento o devuelve NULL si el número de tipos de datos es superior a 32.767.|  
|**variable**|**bit**|Tipo de datos de longitud variable.<br /><br /> 1 = True<br /><br /> 0 = False|  
|**AllowNulls**|**bit**|Indica la nulabilidad predeterminada para este tipo de datos. Se reemplaza el valor predeterminado si la nulabilidad se especifica mediante [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) o [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).|  
|**Tipo**|**tinyint**|Tipo de datos de almacenamiento físico.|  
|**printfmt**|**varchar (255)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**Prec**|**smallint**|Nivel de precisión de este tipo de datos.<br /><br /> -1 = **xml** o tipos de valores grandes.|  
|**escala**|**tinyint**|Escala del tipo de datos, basada en la precisión.<br /><br /> NULL = El tipo de datos no es numérico.|  
|**Intercalación**|**sysname**|Si se basa en caracteres, **intercalación** es la intercalación de la base de datos actual; en caso contrario, es NULL.|  
  
## <a name="see-also"></a>Vea también  
 [Vistas de compatibilidad &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)   
 [Asignar tablas del sistema a vistas del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)  
  
  
