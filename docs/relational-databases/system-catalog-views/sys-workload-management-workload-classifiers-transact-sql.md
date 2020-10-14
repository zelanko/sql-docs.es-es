---
description: sys.workload_management_workload_classifiers (Transact-SQL)
title: sys.workload_management_workload_classifiers (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: 78811f776f7492cdcdba10a0f257e3d9a8f44aa7
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/14/2020
ms.locfileid: "92033938"
---
# <a name="sysworkload_management_workload_classifiers-transact-sql"></a>sys.workload_management_workload_classifiers (Transact-SQL)

[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

 Devuelve los detalles de los clasificadores de carga de trabajo.  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|
|classifier_id|**int**|IDENTIFICADOR único del clasificador. No admite valores NULL||
group_name|**sysname**|Nombre del grupo de cargas de trabajo al que está asignado el clasificador. No admite valores NULL. Se combina con sys.workload_management_workload_groups ||
name|**sysname**|Nombre del clasificador. Debe ser único para la instancia de. No admite valores NULL.||
|importance|**sysname**|Es la importancia relativa de una solicitud en este grupo de cargas de trabajo y entre grupos de cargas de trabajo para los recursos compartidos.  La importancia especificada en el clasificador invalida la configuración de importancia del grupo de cargas de trabajo. Acepta valores NULL.  Cuando es null, se usa la configuración de importancia del grupo de cargas de trabajo.|Low, below_normal, normal (valor predeterminado), above_normal, alto |
|create_time|**datetime**|Hora en que se creó el clasificador. No admite valores NULL.||
modify_time|**datetime**|Hora en que se modificó por última vez el clasificador. No admite valores NULL.||
is_enabled|**bit**|INTERNAL||
|&nbsp;||||
  
## <a name="permissions"></a>Permisos

Requiere el permiso VIEW SERVER STATE.

## <a name="next-steps"></a>Pasos siguientes

 Para obtener una lista de todas las vistas de catálogo de Azure Synapse Analytics y almacenamiento de datos paralelos, consulte [vistas de catálogo de Azure Synapse Analytics y almacenamiento de datos paralelos](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md). Para crear un clasificador de cargas de trabajo, consulte [crear clasificador de cargas de trabajo](../../t-sql/statements/create-workload-classifier-transact-sql.md). Para obtener más información sobre la clasificación de cargas de trabajo, consulte clasificación de la [carga de trabajo](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)
