---
title: Sys.fn_cdc_map_time_to_lsn (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fn_cdc_map_time_to_lsn
- fn_cdc_map_time_to_lsn_TSQL
- sys.fn_cdc_map_time_to_lsn_TSQL
- fn_cdc_map_time_to_lsn
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_map_time_to_lsn
- sys.fn_cdc_map_time_to_lsn
ms.assetid: 6feb051d-77ae-4c93-818a-849fe518d1d4
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c22074e686f9dff1d988d7453c0c546fa6e049b5
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52399939"
---
# <a name="sysfncdcmaptimetolsn-transact-sql"></a>sys.fn_cdc_map_time_to_lsn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el valor de número (LSN) de secuencia de registro desde el **start_lsn** columna en el [cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) tabla del sistema durante el tiempo especificado. Puede usar esta función para asignar sistemáticamente los intervalos de fecha y hora en el intervalo basado en LSN necesario para las funciones de enumeración de captura de datos modificados [cdc.fn_cdc_get_all_changes_ < capture_instance >](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md) y [cdc.fn _cdc_get_net_changes_ < capture_instance >](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md) para devolver los cambios de datos dentro de ese intervalo.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.fn_cdc_map_time_to_lsn ( '<relational_operator>', tracking_time )  
  
<relational_operator> ::=  
{  largest less than  
 | largest less than or equal  
 | smallest greater than  
 | smallest greater than or equal  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 **'**< relational_operator >**'** {más grande menor que | más grande menor que o igual | más pequeño mayor que | más pequeño mayor o igual}  
 Se usa para identificar un valor de LSN distinto dentro de la **cdc.lsn_time_mapping** tabla con un asociado **tran_end_time** que satisfaga la relación cuando se compara con el *tracking_time*  valor.  
  
 *relational_operator* es **nvarchar (30)**.  
  
 *tracking_time*  
 Es el valor de fecha y hora con el que se hará la comparación. *tracking_time* es **datetime**.  
  
## <a name="return-type"></a>Tipo devuelto  
 **binary(10)**  
  
## <a name="remarks"></a>Comentarios  
 Para comprender cómo la **sys.fn_cdc_map_time_lsn** se puede usar para asignar los intervalos de fecha y hora a los intervalos de LSN, considere el siguiente escenario. Suponga que un consumidor desea extraer los datos de cambios cada día. Es decir, el consumidor solo desea obtener los cambios que se han realizado durante un día determinado hasta la medianoche incluida. El límite inferior del intervalo temporal sería hasta las doce de la noche (no inclusive) del día anterior. El límite superior sería hasta las doce de la noche (inclusive) del día en cuestión. El ejemplo siguiente se muestra cómo la función **sys.fn_cdc_map_time_to_lsn** se puede usar para asignar sistemáticamente este intervalo de tiempo en el intervalo basado en LSN que necesitan las funciones de enumeración de captura de datos modificados para devolver todos los cambios dentro de ese intervalo.  
  
 `DECLARE @begin_time datetime, @end_time datetime, @begin_lsn binary(10), @end_lsn binary(10);`  
  
 `SET @begin_time = '2007-01-01 12:00:00.000';`  
  
 `SET @end_time = '2007-01-02 12:00:00.000';`  
  
 `SELECT @begin_lsn = sys.fn_cdc_map_time_to_lsn('smallest greater than', @begin_time);`  
  
 `SELECT @end_lsn = sys.fn_cdc_map_time_to_lsn('largest less than or equal', @end_time);`  
  
 `SELECT * FROM cdc.fn_cdc_get_net_changes_HR_Department(@begin_lsn, @end_lsn, 'all` `');`  
  
 El operador relacional '`smallest greater than`' se usa para restringir los cambios a los que se han producido después de las doce de la noche del día anterior. Si los valores de varias entradas con LSN diferentes comparten el **tran_end_time** valor identificado como límite inferior en el [cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) tabla, la función devolverá el LSN más pequeño, lo que garantiza que se incluyen todas las entradas. Para el límite superior, el operador relacional '`largest less than or equal to`' se utiliza para asegurarse de que el intervalo incluye todas las entradas del día las incluidas que tienen la medianoche como sus **tran_end_time** valor. Si los valores de varias entradas con LSN diferentes comparten el **tran_end_time** valor identificado como límite superior, la función devolverá el LSN más grande, lo que garantiza que se incluyen todas las entradas.  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol **public** .  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa el `sys.fn_cdc_map_time_lsn` para determinar si hay filas en función del [cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) de tabla con un **tran_end_time** valor que es mayor o igual a medianoche. Esta consulta se puede usar para determinar, por ejemplo, si el proceso captura ya ha procesado los cambios confirmados hasta las doce de la noche del día anterior, para que la extracción de los datos cambiados durante ese día pueda llevarse a cabo.  
  
```  
DECLARE @extraction_time datetime, @lsn binary(10);  
SET @extraction_time = '2007-01-01 12:00:00.000';  
SELECT @lsn = sys.fn_cdc_map_time_to_lsn ('smallest greater than or equal', @extraction_time);  
IF @lsn IS NOT NULL  
BEGIN  
<some action>  
END  
```  
  
## <a name="see-also"></a>Vea también  
 [cdc.lsn_time_mapping &#40;Transact-SQL&#41;](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md)   
 [sys.fn_cdc_map_lsn_to_time &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-lsn-to-time-transact-sql.md)   
 [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)  
  
  
