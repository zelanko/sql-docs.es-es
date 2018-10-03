---
title: Sys.fn_cdc_map_lsn_to_time (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_cdc_map_lsn_to_time_TSQL
- sys.fn_cdc_map_lsn_to_time
- fn_cdc_map_lsn_to_time_TSQL
- fn_cdc_map_lsn_to_time
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_cdc_map_lsn_to_time
- fn_cdc_map_lsn_to_time
ms.assetid: 405aa29c-8bd8-42d3-9f39-7494b643fc6f
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 64f5763284ec35caee46565ec596e72870b5631f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47756793"
---
# <a name="sysfncdcmaplsntotime-transact-sql"></a>sys.fn_cdc_map_lsn_to_time (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el valor de fecha y hora desde el **tran_end_time** columna en el [cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) tabla del sistema para el número de secuencia de registro especificado (LSN). Puede usar esta función para asignar sistemáticamente los intervalos del LSN a los intervalos de fechas en una tabla de cambios.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.fn_cdc_map_lsn_to_time ( lsn_value )  
```  
  
## <a name="arguments"></a>Argumentos  
 *lsn_value*  
 Es el valor LSN con el que se debe comparar. *lsn_value* es **binary (10)**.  
  
## <a name="return-type"></a>Tipo devuelto  
 **datetime**  
  
## <a name="remarks"></a>Comentarios  
 Esta función puede utilizarse para determinar el tiempo que un cambio se ha confirmado en función de la **__ $start_lsn** devuelve el valor de la fila de datos modificados.  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol **public** .  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se usa la función `sys.fn_cdc_map_lsn_to_time` para determinar la hora de ejecución asociada al último cambio procesado en el intervalo LSN especificado para la instancia de captura `HumanResources_Employee`.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @max_lsn binary(10);  
SELECT @max_lsn = MAX(__$start_lsn)  
FROM cdc.fn_cdc_get_all_changes_HumanResources_Employee(@from_lsn, @to_lsn, 'all');  
SELECT sys.fn_cdc_map_lsn_to_time(@max_lsn);  
GO   
```  
  
## <a name="see-also"></a>Vea también  
 [cdc.lsn_time_mapping &#40;Transact-SQL&#41;](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)   
 [sys.fn_cdc_map_time_to_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md)   
 [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)  
  
  
