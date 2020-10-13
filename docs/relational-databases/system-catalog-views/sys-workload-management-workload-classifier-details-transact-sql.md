---
description: sys.workload_management_workload_classifier_details (Transact-SQL)
title: sys.workload_management_workload_classifier_details (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: 2135b567509ef9df5f3c8df7a317a9ea45b92ec7
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/13/2020
ms.locfileid: "92006420"
---
# <a name="sysworkload_management_workload_classifier_details-transact-sql"></a>sys.workload_management_workload_classifier_details (Transact-SQL)

[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

  Devuelve los detalles de cada clasificador.  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|
|classifier_id|**int**|IDENTIFICADOR del clasificador.  No admite valores NULL.|
|classifier_type|**sysname**|Se combina con [Sys.workload_management_workload_classifiers](sys-workload-management-workload-classifiers-transact-sql.md).|`membername`</br>`wlm_label`</br>`wlm_context`</br>`start_time`</br>`end_time`|
|classifier_value|**sysname**|Valor del clasificador. No admite valores NULL.||

## <a name="permissions"></a>Permisos

Requiere el permiso VIEW SERVER STATE.

## <a name="next-steps"></a>Pasos siguientes
  
Para obtener una lista de todas las vistas de catálogo de Azure Synapse Analytics y almacenamiento de datos paralelos, consulte [SQL Data Warehouse y las vistas de catálogo de almacenamiento de datos paralelos](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md). Para crear un clasificador de cargas de trabajo, consulte [crear clasificador de cargas de trabajo](../../t-sql/statements/create-workload-classifier-transact-sql.md). Para más información sobre la clasificación de cargas de trabajo, consulte [importancia](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification) de la carga de trabajo y la [clasificación de cargas](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification) de trabajo de Azure Synapse Analytics
