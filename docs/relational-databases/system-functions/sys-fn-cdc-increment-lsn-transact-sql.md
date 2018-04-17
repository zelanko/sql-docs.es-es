---
title: Sys.fn_cdc_increment_lsn (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server (starting with 2008)
f1_keywords:
- fn_cdc_increment_lsn_TSQL
- sys.fn_cdc_increment_lsn_TSQL
- sys.fn_cdc_increment_lsn
- fn_cdc_increment_lsn
dev_langs:
- TSQL
helpviewer_keywords:
- fn_cdc_increment_lsn
- sys.fn_cdc_increment_lsn
ms.assetid: e53b6703-358b-4c9a-912a-8f7c7331069b
caps.latest.revision: 18
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 00925a0374b45ee0eb0fbf1a488858884e465f05
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sysfncdcincrementlsn-transact-sql"></a>sys.fn_cdc_increment_lsn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el número de secuencia de registro (LSN) siguiente de la secuencia basándose en el LSN especificado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.fn_cdc_increment_lsn ( lsn_value )  
```  
  
## <a name="arguments"></a>Argumentos  
 *lsn_value*  
 Valor de LSN. *lsn_value* es **binary (10)**.  
  
## <a name="return-type"></a>Tipo devuelto  
 **binary(10)**  
  
## <a name="remarks"></a>Comentarios  
 El valor LSN devuelto por la función siempre es mayor que el valor especificado y no existe ningún valor LSN entre los dos valores.  
  
 Para consultar sistemáticamente un flujo de datos de cambio durante un periodo de tiempo, puede repetir periódicamente la llamada de función de la consulta, especificando cada vez un nuevo intervalo de la consulta para limitar los cambios devueltos en la misma. Para ayudar a asegurarse de que no se pierden datos, el límite superior de la consulta anterior se utiliza a menudo para generar el límite inferior de la consulta subsiguiente. Dado que el intervalo de la consulta es cerrado, el nuevo límite inferior debe ser mayor que el límite superior anterior, pero lo suficientemente pequeño para asegurarse de que ningún cambio contiene valores LSN comprendidos entre este valor y el límite superior anterior. La función sys.fn_cdc_increment_lsn se utiliza para obtener este valor.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol de base de datos public.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se utiliza `sys.fn_cdc_increment_lsn` para generar un nuevo valor de límite inferior para una consulta de captura de datos modificados basado en el límite superior guardado de una consulta anterior y guardado en la variable `@save_to_lsn`.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @from_lsn binary(10), @to_lsn binary(10), @save_to_lsn binary(10);  
SET @save_to_lsn = <previous_upper_bound_value>;  
SET @from_lsn = sys.fn_cdc_increment_lsn(@save_to_lsn);  
SET @to_lsn = sys.fn_cdc_get_max_lsn();  
SELECT * from cdc.fn_cdc_get_all_changes_HumanResources_Employee( @from_lsn, @to_lsn, 'all' );  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sys.fn_cdc_decrement_lsn &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-cdc-decrement-lsn-transact-sql.md)   
 [cdc.fn_cdc_get_all_changes_&#60;capture_instance&#62;  &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)   
 [cdc.fn_cdc_get_net_changes_&#60;capture_instance&#62; &#40;Transact-SQL&#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [El registro de transacciones &#40;SQL Server&#41;](../../relational-databases/logs/the-transaction-log-sql-server.md)   
 [Acerca de la captura de datos modificados &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md)  
  
  
