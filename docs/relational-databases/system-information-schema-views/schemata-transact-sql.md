---
title: Esquema de datos (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- SCHEMATA_TSQL
- SCHEMATA
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.SCHEMATA view
- SCHEMATA view
ms.assetid: 69617642-0f54-4b25-b62f-5f39c8909601
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: da1a5a26b1d10dca107e7ba061f53ce416348f73
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2019
ms.locfileid: "54129595"
---
# <a name="schemata-transact-sql"></a>SCHEMATA (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve una fila por cada esquema de la base de datos actual. Para recuperar información de estas vistas, especifique el nombre completo de **INFORMATION_SCHEMA.** _view_name_. Para recuperar información acerca de todas las bases de datos en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulta el [sys.databases &#40;Transact-SQL&#41; ](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) vista del catálogo.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**CATALOG_NAME**|**sysname**|Nombre de la base de datos actual|  
|**SCHEMA_NAME**|**nvarchar (** 128 **)**|Devuelve el nombre del esquema.|  
|**SCHEMA_OWNER**|**nvarchar (** 128 **)**|Nombre del propietario del esquema.<br /><br /> **&#42;&#42;Importante &#42; &#42;**  no utilice las vistas INFORMATION_SCHEMA para determinar el esquema de un objeto. La única manera confiable de localizar el esquema de un objeto consiste en consultar la vista de catálogo sys.objects.|  
|**DEFAULT_CHARACTER_SET_CATALOG**|**varchar (** 6 **)**|Siempre devuelve NULL.|  
|**DEFAULT_CHARACTER_SET_SCHEMA**|**varchar (** 3 **)**|Siempre devuelve NULL.|  
|**DEFAULT_CHARACTER_SET_NAME**|**sysname**|Devuelve el nombre del juego de caracteres predeterminado.|  

**Ejemplo**  
El ejemplo siguiente, se devuelve información sobre los esquemas en la base de datos master:  
```sql  
SELECT * FROM master.INFORMATION_SCHEMA.SCHEMATA;
```  

## <a name="see-also"></a>Vea también  
 [Vistas del sistema &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Vistas de esquema de información &#40;Transact-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [sys.schemas &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)   
 [Sys.syscharsets &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syscharsets-transact-sql.md)  
  
  
