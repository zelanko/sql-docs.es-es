---
title: Sys. workload_management_workload_classifiers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/05/2019
ms.prod: sql
ms.technology: system-objects
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: 585eb4551fb688f4f6a620729310b0245462cbff
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "73632965"
---
# <a name="sysworkload_management_workload_classifiers-transact-sql"></a>Sys. workload_management_workload_classifiers (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

 Devuelve los detalles de los clasificadores de carga de trabajo.  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|
|classifier_id|**int**|IDENTIFICADOR único del clasificador. No admite valores NULL||
group_name|**sysname**|Nombre del grupo de cargas de trabajo al que está asignado el clasificador. No admite valores NULL. Se combina con sys. workload_management_workload_groups ||
name|**sysname**|Nombre del clasificador. Debe ser único para la instancia de. No admite valores NULL.||
|importance|**sysname**|Es la importancia relativa de una solicitud en este grupo de cargas de trabajo y entre grupos de cargas de trabajo para los recursos compartidos.  La importancia especificada en el clasificador invalida la configuración de importancia del grupo de cargas de trabajo. Acepta valores NULL.  Cuando es null, se usa la configuración de importancia del grupo de cargas de trabajo.|Low, below_normal, normal (valor predeterminado), above_normal, alto |
|create_time|**datetime**|Hora en que se creó el clasificador. No admite valores NULL.||
modify_time|**datetime**|Hora en que se modificó por última vez el clasificador. No admite valores NULL.||
is_enabled|**bit**|INTERNAL||
|&nbsp;||||
  
## <a name="permissions"></a>Permisos

Requiere el permiso VIEW SERVER STATE.

## <a name="next-steps"></a>Pasos siguientes

 Para obtener una lista de todas las vistas de catálogo para SQL Data Warehouse y almacenamiento de datos paralelos, consulte [SQL Data Warehouse y las vistas de catálogo de almacenamiento de datos paralelas](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md). Para crear un clasificador de cargas de trabajo, consulte [crear clasificador de cargas de trabajo](../../t-sql/statements/create-workload-classifier-transact-sql.md). Para obtener más información sobre la clasificación de cargas de trabajo, consulte clasificación de la [carga de trabajo](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)
