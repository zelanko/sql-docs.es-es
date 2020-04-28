---
title: Sys. check_constraints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/28/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.check_constraints
- sys.check_constraints_TSQL
- check_constraints_TSQL
- check_constraints
dev_langs:
- TSQL
helpviewer_keywords:
- sys.check_constraints catalog view
ms.assetid: 940ebc5e-44ba-4dae-8b29-da94f2d1d6c4
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2212ebe8551f27c880ebf0c674f4b8d134617b07
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67942503"
---
# <a name="syscheck_constraints-transact-sql"></a>sys.check_constraints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Contiene una fila por cada objeto que es una restricción CHECK, con **Sys. Objects. Type** = ' C '.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**\<Columnas heredadas de sys. Objects>**||Para obtener una lista de las columnas que hereda esta vista, vea [Sys. objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).|  
|**is_disabled**|**bit**|La restricción CHECK está deshabilitada.|  
|**is_not_for_replication**|**bit**|La restricción CHECK ha sido creada con la opción NOT FOR REPLICATION.|  
|**is_not_trusted**|**bit**|La restricción CHECK no ha sido comprobada por el sistema para todas las filas.|  
|**parent_column_id**|**int**|0 indica una restricción CHECK de nivel de tabla.<br /><br /> Un valor distinto de cero indica que se trata de una restricción CHECK de nivel de columna definida en la columna con el valor de Id. especificado.|  
|**definir**|**nvarchar(max)**|Expresión SQL que define esta restricción CHECK.|  
|**uses_database_collation**|**bit**|1 = La definición de la restricción depende de la intercalación predeterminada de la base de datos para la evaluación correcta; en caso contrario, 0. Esta dependencia evita el cambio de la intercalación predeterminada de la base de datos.|  
|**is_system_named**|**bit**|1 = El nombre ha sido generado por el sistema.<br /><br /> 0 = El usuario proporcionó el nombre.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo de objetos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
