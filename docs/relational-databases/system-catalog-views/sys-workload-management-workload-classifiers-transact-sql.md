---
title: sys.workload_management_workload_classifiers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2019
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
ms.openlocfilehash: 3b023654728375aee76bfb0c4434a8413dc81e7d
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582568"
---
# <a name="sysworkloadmanagementworkloadclassifiers-transact-sql-preview"></a>sys.workload_management_workload_classifiers (Transact-SQL) (Preview)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

> [!Note]
> Clasificación de la carga de trabajo está disponible para vista previa en SQL Data Warehouse Gen2. Clasificación de la administración de cargas de trabajo y la importancia de vista previa es para las compilaciones con una fecha de lanzamiento de 9 de abril de 2019 o posterior.  Los usuarios deben evitar usar compilaciones anteriores a esta fecha para pruebas de carga de trabajo administración.  Para determinar si la compilación es capaz de administración de cargas de trabajo, ejecutar select @@version cuando se conecta a la instancia de SQL Data Warehouse.

 Devuelve los detalles de clasificadores de carga de trabajo.  
  
|Nombre de la columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|
|classifier_id|**int**|Id. exclusivo del clasificador. No admite valores NULL||
group_name|**sysname**|Se asigna a nombre del grupo de cargas de trabajo del clasificador. No admite valores NULL. |Clases de recursos estáticos</br>staticrc10</br>staticrc20</br>staticrc30</br>staticrc40</br>staticrc50</br>staticrc60</br>staticrc70</br>staticrc80 </br> </br>Clases de recursos dinámicos</br>smallrc</br>mediumrc</br>largerc</br>xlargerc|
NAME|**sysname**|Nombre del clasificador. Debe ser único para la instancia. No admite valores NULL.||
|importance|**sysname**|Es la importancia relativa de una solicitud de este grupo de cargas de trabajo y a través de grupos de cargas de trabajo para los recursos compartidos.  Importancia especificada en el clasificador invalida la configuración de importancia del grupo de cargas de trabajo.|bajo, below_normal, normal, above_normal, alto |
|create_time|**datetime**|Hora de que creación del clasificador. No admite valores NULL.||
modify_time|**datetime**|Hora de que última modificación el clasificador. No admite valores NULL.||
is_enabled|**bit**|Muestra si el clasificador está habilitado o no. Está habilitado de forma predeterminada. No admite valores NULL.|0 = no está habilitado el clasificador </br> 1 = el clasificador está habilitado|
|&nbsp;||||
  
## <a name="permissions"></a>Permisos

Requiere el permiso VIEW SERVER STATE.

## <a name="next-steps"></a>Pasos siguientes

 Para obtener una lista de todas las vistas de catálogo para SQL Data Warehouse y almacenamiento de datos paralelos, vea [SQL Data Warehouse y vistas de catálogo de almacén de datos paralelo](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md). Para crear un clasificador de carga de trabajo, consulte [crear CLASIFICADOR de carga de trabajo](../../t-sql/statements/create-workload-classifier-transact-sql.md). Para obtener más información sobre la clasificación de la carga de trabajo, consulte [clasificación de carga de trabajo de almacenamiento de datos de SQL](/azure/sql-data-warehouse/sql-data-warehouse-workload-classification)
