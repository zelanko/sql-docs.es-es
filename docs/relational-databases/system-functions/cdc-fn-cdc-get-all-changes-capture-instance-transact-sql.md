---
title: CDC.fn_cdc_get_all_changes_&lt;capture_instance&gt; (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_get_all_changes_<capture_instance>
- change data capture [SQL Server], querying metadata
- cdc.fn_cdc_get_all_changes_<capture_instance>
ms.assetid: c6bad147-1449-4e20-a42e-b51aed76963c
author: rothja
ms.author: jroth
ms.openlocfilehash: 0a4e0e62121d289f9eb897c79abb2991a57890a4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68043051"
---
# <a name="cdcfncdcgetallchangesltcaptureinstancegt--transact-sql"></a>cdc.fn_cdc_get_all_changes_&lt;capture_instance&gt;  (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve una fila para cada cambio aplicado a la tabla de origen dentro del intervalo del número de secuencia de registro (LSN) especificado. Si una fila de origen ha tenido muchos cambios durante el intervalo, cada cambio se representa en el conjunto de resultados devuelto. Además de devolver los datos del cambio, cuatro columnas de metadatos proporcionan la información que necesita aplicar los cambios a otro origen de datos. Las opciones de filtrado de filas rigen el contenido de las columnas de metadatos y de las filas devueltas en el conjunto de resultados. Cuando se especifica la opción de filtro de filas 'all', cada cambio tiene exactamente una fila para identificar el cambio. Cuando se especifica la opción 'all update old', las operaciones de actualización se representan como dos filas: una que contiene los valores de las columnas capturadas antes de la actualización y otra que contiene los valores de las columnas capturadas después de la actualización.  
  
 Esta función de enumeración se crea cuando se habilita una tabla de origen para la captura de datos modificados. Usa el formato y se obtiene el nombre de función **cdc.fn_cdc_get_all_changes_** _capture_instance_ donde *capture_instance* es el valor especificado para la captura instancia de la tabla de origen está habilitada para la captura de datos modificados.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
cdc.fn_cdc_get_all_changes_capture_instance ( from_lsn , to_lsn , '<row_filter_option>' )  
  
<row_filter_option> ::=  
{ all  
 | all update old  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 *from_lsn*  
 Establezca el valor LSN que representa el extremo inferior del intervalo LSN para incluir en el resultado. *from_lsn* es **binary (10)** .  
  
 Solo las filas de la [cdc.&#91; capture_instance&#93;_CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md) cambiar la tabla con un valor en **__ $start_lsn** mayor o igual a *from_lsn* se incluyen en el conjunto de resultados.  
  
 *to_lsn*  
 El valor LSN que representa el extremo inferior del rango de LSN que se incluirá en el conjunto de resultados. *to_lsn* es **binary (10)** .  
  
 Solo las filas de la [cdc.&#91; capture_instance&#93;_CT](../../relational-databases/system-tables/cdc-capture-instance-ct-transact-sql.md) cambiar la tabla con un valor en **__ $start_lsn** menor o igual a *from_lsn* o igual que *to_lsn* se incluyen en el conjunto de resultados.  
  
 <row_filter_option> ::= { all | all update old }  
 Una opción que rige el contenido de las columnas de metadatos y las filas devueltas en el conjunto de resultados.  
  
 Puede ser una de las siguientes opciones:  
  
 all  
 Devuelve todos los cambios dentro del intervalo LSN especificado. Para los cambios debidos a una operación de actualización, esta opción devuelve solo la fila que contiene los nuevos valores una vez aplicada la actualización.  
  
 all update old  
 Devuelve todos los cambios dentro del intervalo LSN especificado. Para los cambios debidos a una operación de actualización, esta opción devuelve tanto la fila que contiene los nuevos valores antes de la actualización como la fila que contiene los valores de columna después de la actualización.  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**__$start_lsn**|**binary(10)**|LSN de confirmación asociado con el cambio que conserva el orden de confirmación del cambio. Los cambios confirmados en la misma transacción comparten el mismo valor LSN de confirmación.|  
|**__$seqval**|**binary(10)**|Valor de secuencia utilizado para ordenar los cambios en una fila dentro de una transacción.|  
|**__$operation**|**int**|Identifica la operación del lenguaje de manipulación de datos (DML) necesaria para aplicar la fila de datos modificados al origen de datos de destino. Puede ser uno de los valores siguientes:<br /><br /> 1 = eliminar<br /><br /> 2 = insertar<br /><br /> 3 = actualización (los valores de columna capturados son los de antes de la operación de actualización). Este valor solamente se aplica cuando se especifica la opción de filtro de filas 'all update old'.<br /><br /> 4 = actualización (los valores de columna capturados son los de después de la operación de actualización)|  
|**__$update_mask**|**varbinary(128)**|Máscara de bits con un bit que corresponde a cada columna capturada identificada para la instancia de captura. Este valor tiene todos los bits definidos establecidos en 1 cuando **__ $operation** = 1 o 2. Cuando **__ $operation** = 3 o 4, solo los bits que corresponden a columnas que han cambiado se establecen en 1.|  
|**\<columnas de la tabla de origen capturadas>**|varía|Las columnas restantes devueltas por la función son las columnas capturadas identificadas cuando se creó la instancia de captura. Si no se especificó ninguna columna en la lista de columnas capturadas, se devuelven todas las columnas de la tabla de origen.|  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer a la **sysadmin** rol fijo de servidor o **db_owner** rol fijo de base de datos. Para el resto de usuarios, requiere el permiso SELECT en todas las columnas capturadas en la tabla de origen y, si se ha definido un rol de acceso para la instancia de captura, la pertenencia a ese rol de base de datos. Cuando el llamador no tiene permiso para ver los datos de origen, la función devuelve el error 229 ("se denegó el permiso SELECT en el objeto 'fn_cdc_get_all_changes_...', base de datos '\<nombreBaseDeDatos >', esquema 'cdc'.").  
  
## <a name="remarks"></a>Comentarios  
 Si el intervalo de LSN especificado no cae dentro de la escala de tiempo del seguimiento de cambios de la instancia de captura, la función devuelve el error 208 ("Se ha especificado un número insuficiente de argumentos para el procedimiento o la función cdc.fn_cdc_get_all_changes".).  
  
 Las columnas de tipo de datos **imagen**, **texto**, y **ntext** siempre se les asigna un valor NULL al valor **__ $operation** = 1 o **__ $ operación** = 3. Las columnas de tipo de datos **varbinary (max)** , **varchar (max)** , o **nvarchar (max)** se asignan un valor NULL al valor **__ $operation** = 3 a menos que la columna cambie durante la actualización. Cuando **__ $operation** = 1, estas columnas se les asigna su valor en el momento de la eliminación. Las columnas calculadas que están incluidas en una instancia de captura siempre tienen el valor NULL.  
  
## <a name="examples"></a>Ejemplos  
 Varias [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] existen plantillas que muestran cómo utilizar las funciones de consulta de captura de datos modificados. Estas plantillas están disponibles en el **vista** menú [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Para obtener más información, consulte [Explorador de plantillas](../../ssms/template/template-explorer.md).  
  
 Este ejemplo muestra la `Enumerate All Changes for Valid Range Template`. Utiliza la función `cdc.fn_cdc_get_all_changes_HR_Department` para notificar todos los cambios disponibles actualmente para la instancia de captura `HR_Department`, que se define para la tabla de origen HumanResources.Department de la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
-- ========  
-- Enumerate All Changes for Valid Range Template  
-- ========  
USE AdventureWorks2012;  
GO  
  
DECLARE @from_lsn binary(10), @to_lsn binary(10);  
SET @from_lsn = sys.fn_cdc_get_min_lsn('HR_Department');  
SET @to_lsn   = sys.fn_cdc_get_max_lsn();  
SELECT * FROM cdc.fn_cdc_get_all_changes_HR_Department  
  (@from_lsn, @to_lsn, N'all');  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [sys.fn_cdc_map_time_to_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-map-time-to-lsn-transact-sql.md)   
 [sys.sp_cdc_get_ddl_history &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-ddl-history-transact-sql.md)   
 [sys.sp_cdc_get_captured_columns &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-get-captured-columns-transact-sql.md)   
 [sys.sp_cdc_help_change_data_capture &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [Acerca de la captura de datos modificados &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
