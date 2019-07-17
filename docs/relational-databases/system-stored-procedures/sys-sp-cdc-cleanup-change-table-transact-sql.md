---
title: sys.sp_cdc_cleanup_change_table (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cdc_cleanup_change_table
- sp_cdc_cleanup_change_table_TSQL
- sys.sp_cdc_cleanup_change_table
- sys.sp_cdc_cleanup_change_table_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_cdc_cleanup_change_tables
- sp_cdc_cleanup_change_tables
ms.assetid: 02295794-397d-4445-a3e3-971b25e7068d
author: rothja
ms.author: jroth
ms.openlocfilehash: dcf68e23652eb81e163722f69d9645c7502af5b9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68106520"
---
# <a name="sysspcdccleanupchangetable-transact-sql"></a>sys.sp_cdc_cleanup_change_table (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita las filas de la tabla de cambios en la base de datos según lo especificado *low_water_mark* valor. Este procedimiento almacenado se proporciona a los usuarios que desean administrar directamente la proceso de limpieza de las tablas de cambios. Sin embargo, se debe utilizar con precaución, porque el procedimiento afecta a todos los consumidores de los datos en la tabla de cambios.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.sp_cdc_cleanup_change_table   
  [ @capture_instance = ] 'capture_instance',   
  [ @low_water_mark = ] low_water_mark ,  
  [ @threshold = ]'delete threshold'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @capture_instance =] '*capture_instance*'  
 Es el nombre de la instancia de captura asociada a la tabla de cambios. *capture_instance* es **sysname**, no tiene ningún valor predeterminado, y no puede ser NULL.  
  
 *capture_instance* debe asignar nombre a una instancia de captura que exista en la base de datos actual.  
  
 [ @low_water_mark =] *low_water_mark*  
 Es un número de secuencia de registro (LSN) que se utiliza como el nuevo límite inferior para el *instancia de captura*. *low_water_mark* es **binary (10)** , no tiene ningún valor predeterminado.  
  
 Si el valor no es null, debe aparecer como el valor start_lsn de una entrada actual en el [cdc.lsn_time_mapping](../../relational-databases/system-tables/cdc-lsn-time-mapping-transact-sql.md) tabla. Si otras entradas de cdc.lsn_time_mapping comparten la misma la hora de confirmación que la entrada identificada por el nuevo límite inferior, el LSN más pequeño asociado a dicho grupo de entradas se elige como límite inferior.  
  
 Si el valor se establece explícitamente en NULL, actual *límite mínimo* para el *instancia de captura* se utiliza para definir el límite superior para la operación de limpieza.  
  
 [ @threshold=] '*eliminar umbral*'  
 Es el número máximo de entradas de eliminación que se pueden eliminar mediante el uso de una única instrucción en el proceso de limpieza. *delete_threshold* es **bigint**, su valor predeterminado es 5000.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 sys.sp_cdc_cleanup_change_table realiza las operaciones siguientes:  
  
1.  Si el @low_water_mark parámetro no es NULL, Establece el valor de start_lsn para la *instancia de captura* al nuevo *límite mínimo*.  
  
    > [!NOTE]  
    >  El nuevo límite mínimo puede no ser el límite mínimo que se especifica en la llamada al procedimiento almacenado. Si otras entradas de la tabla cdc.lsn_time_mapping tienen la misma hora de confirmación, se selecciona el valor start_lsn menor representado en el grupo de entradas como el límite mínimo ajustado. Si el @low_water_mark parámetro es NULL o el límite mínimo actual es mayor que el nuevo límite mínimo, el valor start_lsn de la instancia de captura permanece sin cambios.  
  
2.  A continuación, se eliminan las entradas de la tabla de cambios con valores de __$start_lsn menores que el límite mínimo. El umbral de eliminación se utiliza para limitar el número de filas eliminadas en una sola transacción. Si no se pueden eliminar correctamente las entradas, se notifica, pero esto no afecta a ningún cambio en el límite mínimo de la instancia de captura que se haya realizado con la llamada.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

 Utilice sys.sp_cdc_cleanup_change_table en las circunstancias siguientes:  
  
-   El agente de limpieza notifica errores de eliminación.  
  
     Un administrador puede ejecutar explícitamente este procedimiento almacenado para reintentar una operación que no se ha ejecutado correctamente. Para volver a intentar la limpieza para una instancia de captura determinada, ejecute sys.sp_cdc_cleanup_change_table y especifique NULL para el @low_water_mark parámetro.  
  
-   La directiva simple basada en retención utilizada por el trabajo del agente de limpieza no es correcta.  
  
     Como este procedimiento almacenado realiza la limpieza para una instancia de captura única, se puede utilizar para generar una estrategia de limpieza personalizada que se adapte a las reglas de limpieza de cada instancia de captura.  
  
## <a name="permissions"></a>Permisos  
 Requiere pertenencia al rol fijo de base de datos db_owner.  
  
## <a name="see-also"></a>Vea también  
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)   
 [sys.fn_cdc_get_min_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-get-min-lsn-transact-sql.md)   
 [sys.fn_cdc_increment_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-increment-lsn-transact-sql.md)  
  
  
