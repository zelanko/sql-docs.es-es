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
ms.openlocfilehash: 9afd00a887244c02849d40eed635500b06533709
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582728"
---
# <a name="sysworkloadmanagementworkloadclassifierdetails-transact-sql-preview"></a>sys.workload_management_workload_classifier_details (Transact-SQL) (Preview)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

> [!Note]
> Clasificación de la carga de trabajo está disponible para vista previa en SQL Data Warehouse Gen2. Clasificación de la administración de cargas de trabajo y la importancia de vista previa es para las compilaciones con una fecha de lanzamiento de 9 de abril de 2019 o posterior.  Los usuarios deben evitar usar compilaciones anteriores a esta fecha para pruebas de carga de trabajo administración.  Para determinar si la compilación es capaz de administración de cargas de trabajo, ejecutar select @@version cuando se conecta a la instancia de SQL Data Warehouse.

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
