---
title: sys.workload_management_workload_classifier_details (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/26/2019
ms.prod: ''
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.topic: language-reference
dev_langs:
- TSQL
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: ed7694f087a8e1b10697ed2083dbae8bf879528c
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58513312"
---
# <a name="sysworkloadmanagementworkloadclassifierdetails-transact-sql-preview"></a>sys.workload_management_workload_classifier_details (Transact-SQL) (Preview)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

  Devuelve los detalles de cada clasificador.  
  
|Nombre de la columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|
|classifier_id|**int**|Id. del clasificador. Puede unir a [sys.workload_management_workload_classifiers](sys-workload-management-workload-classifiers-transact-sql.md). No admite valores NULL.|
|classifier_type|**sysname**|La entidad en el que se realiza la clasificación. No admite valores NULL.|MEMBERNAME|
|classifier_value|**sysname**|El valor del clasificador. No admite valores NULL.||

## <a name="permissions"></a>Permisos

Requiere el permiso VIEW SERVER STATE.

## <a name="next-steps"></a>Pasos siguientes
  
 Para obtener una lista de todas las vistas de catálogo para SQL Data Warehouse y almacenamiento de datos paralelos, vea [SQL Data Warehouse y vistas de catálogo de almacén de datos paralelo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md). Para crear un clasificador de carga de trabajo, consulte [crear CLASIFICADOR de carga de trabajo](../../t-sql/statements/create-workload-classifier-transact-sql.md). Para obtener más información sobre la clasificación de la carga de trabajo, consulte SQL Data Warehouse [clasificación de la carga de trabajo](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification) y [importancia de la carga de trabajo](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)
