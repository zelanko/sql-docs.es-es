---
title: Sys.fn_cdc_get_column_ordinal (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/25/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_cdc_get_column_ordinal
- fn_cdc_get_column_ordinal_TSQL
- fn_cdc_get_column_ordinal
- sys.fn_cdc_get_column_ordinal_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_get_column_ordinal
- sys.fn_cdc_get_column_ordinal
ms.assetid: 4bb21a57-2b94-4208-8bdf-6a3e2681d881
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: a3170d1b191538f23b374a59af19084effa73e81
ms.sourcegitcommit: 5d6e1c827752c3aa2d02c4c7653aefb2736fffc3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/10/2018
ms.locfileid: "49072019"
---
# <a name="sysfncdcgetcolumnordinal-transact-sql"></a>sys.fn_cdc_get_column_ordinal (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el ordinal de columna de la columna especificada tal y como aparece en el [cambiar tabla](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md) asociado a la instancia de captura especificada.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.fn_cdc_get_column_ordinal ( 'capture_instance','column_name')  
```  
  
## <a name="arguments"></a>Argumentos  
 **'** *capture_instance* **'**  
 Es el nombre de la instancia de captura en la que la columna especificada está identificada como columna capturada. *capture_instance* es **sysname**.  
  
 **'** *column_name* **'**  
 Es la columna para la que se creará un informe. *column_name* es **sysname**.  
  
## <a name="return-type"></a>Tipo devuelto  
 **int**  
  
## <a name="remarks"></a>Comentarios  
 Esta función se utiliza para identificar la posición ordinal de una columna capturada dentro de la máscara de actualización de la captura de datos modificados. Se utiliza principalmente junto con la función [sys.fn_cdc_is_bit_set](../../relational-databases/system-functions/sys-fn-cdc-is-bit-set-transact-sql.md) para extraer información de la máscara de actualización al consultar datos modificados.  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso SELECT en todas las columnas capturadas de la tabla de origen. Si se especifica un rol de base de datos en la captura de datos de cambio para la instancia de captura, también se requiere la pertenencia a ese rol.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se obtiene la posición ordinal de la columna `VacationHours` en la máscara de actualización de la instancia de captura `HumanResources_Employee`. Este valor se utiliza a continuación en la llamada a `sys.fn_cdc_is_bit_set` para extraer información de la máscara de actualización devuelta.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @from_lsn binary(10), @to_lsn binary(10),  @VacationHoursOrdinal int;  
SET @from_lsn = sys.fn_cdc_get_min_lsn('HumanResources_Employee');  
SET @to_lsn = sys.fn_cdc_get_max_lsn();  
SET @VacationHoursOrdinal = sys.fn_cdc_get_column_ordinal   
    ( 'HumanResources_Employee','VacationHours');  
SELECT *, sys.fn_cdc_is_bit_set(@VacationHoursOrdinal,  
    __$update_mask) as 'VacationHours'  
FROM cdc.fn_cdc_get_net_changes_HumanResources_Employee  
    ( @from_lsn, @to_lsn, 'all with mask');  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones de captura de datos modificados &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-data-capture-functions-transact-sql.md)   
 [Acerca de la captura de datos modificados &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)   
 [sys.sp_cdc_help_change_data_capture &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [sys.sp_cdc_get_captured_columns &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-captured-columns-transact-sql.md)   
 [sys.fn_cdc_is_bit_set &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-is-bit-set-transact-sql.md)  
  
  
