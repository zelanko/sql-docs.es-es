---
title: Sys. pdw_column_distribution_properties (Transact-SQL)
ms.custom: seo-dt-2019
ms.date: 03/03/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 46b74f99-2e22-4dbd-872a-533fce0e239c
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: c68c2782a7aaed19edd4e24e04e19b90bdf67800
ms.sourcegitcommit: 01297f2487fe017760adcc6db5d1df2c1234abb4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/09/2020
ms.locfileid: "86196966"
---
# <a name="syspdw_column_distribution_properties-transact-sql"></a>Sys. pdw_column_distribution_properties (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Contiene información de distribución para las columnas.  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|**object_id**|**int**|IDENTIFICADOR del objeto al que pertenece la columna.||  
|**column_id**|**int**|Identificador de la columna.||  
|**distribution_ordinal**|**tinyint**|Ordinal (de base 1) dentro del conjunto de distribución.|0 = no es una columna de distribución. 1 = [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] está usando esta columna para distribuir la tabla primaria.|  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo de SQL Data Warehouse y Almacenamiento de datos paralelos](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
