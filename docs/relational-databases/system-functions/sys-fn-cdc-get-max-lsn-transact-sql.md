---
title: Sys.fn_cdc_get_max_lsn (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server (starting with 2008)
f1_keywords:
- sys.fn_cdc_get_max_lsn
- fn_cdc_get_max_lsn
- fn_cdc_get_max_lsn_TSQL
- sys.fn_cdc_get_max_lsn_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_get_max_lsn
- sys.fn_cdc_get_max_lsn
ms.assetid: 93f3a4c8-b91f-4ebb-8e96-9397bb3a1c43
caps.latest.revision: 15
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 5ef48731e0e333d39b24235e848ac497cd59c19f
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="sysfncdcgetmaxlsn-transact-sql"></a>sys.fn_cdc_get_max_lsn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el número de secuencia de registro máximo (LSN) de la columna start_lsn de la [cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) tabla del sistema. Puede utilizar esta función para devolver el extremo alto de la escala de tiempo de captura de los datos del cambio para cualquier instancia de captura.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.fn_cdc_get_max_lsn ()  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 **binary(10)**  
  
## <a name="remarks"></a>Comentarios  
 Esta función devuelve el LSN máximo en la columna start_lsn de la [cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) tabla. Por tanto, es el último LSN procesado por el proceso de captura cuando los cambios se propagan a las tablas de cambios de base de datos. Actúa como extremo superior para todas las escalas de tiempo asociadas con las instancias de captura definidas para la base de datos.  
  
 La función se utiliza normalmente para obtener un extremo final superior adecuado para un intervalo de consulta.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol de base de datos public.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-returning-the-maximum-lsn-value"></a>A. Devolver el valor LSN máximo  
 El ejemplo siguiente devuelve el LSN máximo para todas las instancias de captura en la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```  
USE AdventureWorks2012;  
GO  
SELECT sys.fn_cdc_get_max_lsn()AS max_lsn;  
```  
  
### <a name="b-setting-the-high-endpoint-of-a-query-range"></a>B. Establecer el extremo alto de un rango de la consulta  
 El ejemplo siguiente utiliza el LSN máximo devuelto por `sys.fn_cdc_get_max_lsn` para establecer el extremo alto para un intervalo de consultas para la instancia de captura `HumanResources_Employee`.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @from_lsn binary(10), @to_lsn binary(10);  
SET @from_lsn = sys.fn_cdc_get_min_lsn(N'HumanResources_Employee');  
SET @to_lsn = sys.fn_cdc_get_max_lsn();  
SELECT * FROM cdc.fn_cdc_get_all_changes_HumanResources_Employee(@from_lsn, @to_lsn, 'all');  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sys.fn_cdc_get_min_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql.md)   
 [El registro de transacciones &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)  
  
  
