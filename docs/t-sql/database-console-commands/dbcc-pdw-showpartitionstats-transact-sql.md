---
description: DBCC PDW_SHOWPARTITIONSTATS (Transact-SQL)
title: DBCC PDW_SHOWPARTITIONSTATS (Transact-SQL)
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
author: pmasl
ms.author: umajay
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 03ef74fb824c39aee0045f378f6aaf5268052794
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88479844"
---
# <a name="dbcc-pdw_showpartitionstats-transact-sql"></a>DBCC PDW_SHOWPARTITIONSTATS (Transact-SQL)

[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

Muestra el tamaño y el número de filas de cada partición de una tabla en una base de datos [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].
  
![Icono de vínculo al artículo](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de artículo") [Convenciones de sintaxis de Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```syntaxsql
Show the partition stats for a table  
DBCC PDW_SHOWPARTITIONSTATS ( " [ database_name . [ schema_name ] . ] | [ schema_name.] table_name  ")  
[;]  
```  

## <a name="arguments"></a>Argumentos  
 `[ database_name . [ schema_name ] . | schema_name . ] table_name`  
 Nombre de una, dos o tres partes de la tabla que se va a mostrar.  En el caso de los nombres de tabla de dos o tres partes, el nombre debe incluirse entre comillas dobles (""). El uso de comillas en un nombre de tabla de una parte es opcional.  
  
## <a name="permissions"></a>Permisos
Requiere el permiso **VIEW SERVER STATE**.
  
## <a name="result-sets"></a>Conjuntos de resultados  
Este conjunto es el resultado del comando DBCC PDW_SHOWPARTITIONSTATS.
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|partition_number|int|Número de partición.|  
|used_page_count|bigint|Número de páginas usadas para los datos.|  
|reserved_page_count|bigint|Número de páginas reservadas para la partición.|  
|row_count|bigint|Número de filas de la partición.|  
|pdw_node_id|int|Nodo de proceso de los datos.|  
|distribution_id|int|Identificador de distribución de los datos.|  
  
## <a name="examples-sssdw-and-sspdw"></a>Ejemplos: [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
### <a name="a-dbcc-pdw_showpartitionstats-basic-syntax-examples"></a>A. Ejemplos de sintaxis básica de DBCC PDW_SHOWPARTITIONSTATS  
Los ejemplos siguientes muestran el espacio usado y el número de filas por partición de la tabla FactInternetSales de la base de datos [!INCLUDE[ssawPDW](../../includes/ssawpdw-md.md)].
  
```sql
DBCC PDW_SHOWPARTITIONSTATS ("ssawPDW.dbo.FactInternetSales");  
DBCC PDW_SHOWPARTITIONSTATS ("dbo.FactInternetSales");  
DBCC PDW_SHOWPARTITIONSTATS (FactInternetSales);  
```  

## <a name="see-also"></a>Consulte también

- [DBCC PDW_SHOWEXECUTIONPLAN &#40;Transact-SQL&#41;](dbcc-pdw-showexecutionplan-transact-sql.md)  
- [DBCC PDW_SHOWSPACEUSED &#40;Transact-SQL&#41;](dbcc-pdw-showspaceused-transact-sql.md)  
