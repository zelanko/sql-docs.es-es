---
title: Sys.pdw_nodes_tables (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 473b5d14-171b-4a16-9195-acf36d3f786c
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: a8d89adf13e2e377122321fd8e385b96888e699e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47817483"
---
# <a name="syspdwnodestables-transact-sql"></a>Sys.pdw_nodes_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  Contiene una fila para cada objeto de tabla que son propiedad de una entidad de seguridad o en el que la entidad de seguridad tiene algún permiso.  
  
|Nombre de la columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|\<hereda columnas >||Para obtener una lista de columnas que hereda esta vista, consulte [sys.objects](http://msdn.microsoft.com/c36fa71e-549a-4533-a6cd-1314d26f533f).||  
|lob_data_space_id|**int**||Siempre es 0.|  
|filestream_data_space_id|**int**|Id. de espacio de datos para un grupo de archivos FILESTREAM o [!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]|NULL|  
|max_column_id_used|**int**|Id. de columna máximo utilizado en esta tabla.||  
|lock_on_bulk_load|**bit**|La tabla está bloqueada en una carga masiva.|TBD|  
|uses_ansi_nulls|**bit**|La tabla se creó con la opción de base de datos SET ANSI_NULLS establecida en ON.|1|  
|is_replicated|**bit**|1 = tabla se publica mediante replicación.|0; no se admite la replicación.|  
|has_replication_filter|**bit**|1 = La tabla tiene un filtro de replicación.|0|  
|is_merge_published|**bit**|1 = La tabla se publicó con la replicación de mezcla.|0; no se admite.|  
|is_sync_tran_subscribed|**bit**|1 = La tabla se suscribió con una suscripción de actualización inmediata.|0; no se admite.|  
|has_unchecked_assembly_data|**bit**|1 = La tabla contiene datos persistentes que dependen de un ensamblado cuya definición cambió durante el último ALTER ASSEMBLY. Se restablecerá en 0 tras la siguiente operación DBCC CHECKDB o DBCC CHECKTABLE correcta.|0; no compatible con CLR.|  
|text_in_row_limit|**int**|0 = el texto de fila no se establece la opción.|Siempre es 0.|  
|large_value_types_out_of_row|**bit**|1 = Los tipos de valores grandes se guardan fuera de la fila.|Siempre es 0.|  
|is_tracked_by_cdc|**bit**|1 = tabla está habilitada para la captura de datos modificados|Siempre es 0; no se admite CDC.|  
|lock_escalation|**tinyint**|El valor de la opción LOCK_ESCALATION para la tabla: 2 = AUTO|Siempre 2.|  
|lock_escalation_desc|**nvarchar(60)**|Descripción de texto de la opción lock_escalation.|Siempre ꞌAUTOꞌ.|  
|pdw_node_id|**int**|Identificador único de un [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] nodo.|NOT NULL|  
  
## <a name="see-also"></a>Vea también  
 [SQL Data Warehouse y vistas de catálogo del almacén de datos en paralelo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
