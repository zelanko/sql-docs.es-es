---
description: sys.pdw_table_distribution_properties (Transact-SQL)
title: sys.pdw_table_distribution_properties (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 639a7475-7c92-41e0-a8ab-ad630eb5aea3
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest'
ms.openlocfilehash: e5a4c129ab6224872293e5bd4cfd9a1b87a378f5
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97412053"
---
# <a name="syspdw_table_distribution_properties-transact-sql"></a>sys.pdw_table_distribution_properties (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Contiene información de distribución para las tablas.  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|**object_id**|**int**|IDENTIFICADOR de la tabla para la que se especificaron las propiedades.||  
|**distribution_policy**|**tinyint**|0 = SIN DEFINIR<br /><br /> 1 = NINGUNO<br /><br /> 2 = HASH<br /><br /> 3 = REPLICAR<br /><br /> 4 = ROUND_ROBIN||  
|**distribution_policy_desc**|**nvarchar(60)**|UNDEFINED, NONE, HASH, REPLICATE, ROUND_ROBIN|[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] Devuelve HASH, ROUND_ROBIN o REPLICAte.|  
  
## <a name="see-also"></a>Consulte también  
 [Vistas de catálogo de Azure Synapse Analytics y Almacenamiento de datos paralelos](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
