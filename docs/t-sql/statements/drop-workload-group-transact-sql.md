---
title: DROP WORKLOAD GROUP (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 11/04/2019
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP_WORKLOAD_GROUP_TSQL
- DROP WORKLOAD GROUP
dev_langs:
- TSQL
helpviewer_keywords:
- DROP WORKLOAD GROUP statement
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azure-sqldw-latest||=azuresqldb-mi-current'
ms.openlocfilehash: 90622710b19ef3c2692cdcff62089cb7539fcf97
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632807"
---
# <a name="drop-workload-group-transact-sql"></a>DROP WORKLOAD GROUP (Transact-SQL)

## <a name="click-a-product"></a>Haga clic en un producto.

En la siguiente fila, haga clic en cualquier nombre de producto que le interese. Al hacer clic, en esta página web se muestra otro contenido, adecuado para el producto que seleccione.

::: moniker range=">=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||=sqlallproducts-allversions"

> |||||
> |---|---|---|---|
> |**\* _SQL Server \*_** &nbsp;|[Instancia administrada de<br />SQL Database](drop-workload-group-transact-sql.md?view=azuresqldb-mi-current)|[SQL Data<br />Warehouse](drop-workload-group-transact-sql.md?view=azure-sqldw-latest)|

&nbsp;

## <a name="sql-server-and-sql-database-managed-instance"></a>Instancia administrada de SQL Server y SQL Database


  Quita un grupo de cargas de trabajo del regulador de recursos definido por el usuario existente.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo a temas") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DROP WORKLOAD GROUP group_name  
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 *group_name*  
 Es el nombre de un grupo de cargas de trabajo definido por el usuario existente.  
  
## <a name="remarks"></a>Notas  
 La instrucción DROP WORKLOAD GROUP no se permite en los grupos predeterminados o internos del regulador de recursos.  
  
 Si va a ejecutar instrucciones de DDL, se recomienda familiarizarse primero con los estados del regulador de recursos. Para obtener más información, vea [Resource Governor](../../relational-databases/resource-governor/resource-governor.md).  
  
 Si un grupo de cargas de trabajo contiene sesiones activas, no se podrá quitar ni mover el grupo de cargas de trabajo a otro grupo de recursos de servidor si se llama a la instrucción ALTER RESOURCE GOVERNOR RECONFIGURE para aplicar el cambio. Para evitar este problema, puede realizar una de las siguientes acciones:  
  
-   Espere hasta que se hayan desconectado todas las sesiones en el grupo afectado y, a continuación, vuelve a ejecutar la instrucción ALTER RESOURCE GOVERNOR RECONFIGURE.  
  
-   Detenga explícitamente las sesiones en el grupo afectado mediante el comando KILL y, a continuación, vuelva a ejecutar la instrucción ALTER RESOURCE GOVERNOR RECONFIGURE.  
  
-   Reinicie el servidor. Una vez completado el proceso del reinicio, no se creará el grupo eliminado y un grupo movido utilizará la nueva asignación del grupo de recursos de servidor.  
  
-   En un escenario en el que ha emitido la instrucción DROP WORKLOAD GROUP pero no desea detener explícitamente las sesiones para aplicar el cambio, puede recrear el grupo si utiliza el mismo nombre que tenía antes de emitir la instrucción DROP y, a continuación, mueve el grupo al grupo de recursos de servidor original. Para aplicar los cambios, ejecute la instrucción ALTER RESOURCE GOVERNOR RECONFIGURE.  
  
## <a name="permissions"></a>Permisos

 Requiere el permiso CONTROL SERVER.  
  
## <a name="examples"></a>Ejemplos

 En el ejemplo siguiente se quita el grupo de cargas de trabajo denominado `adhoc`.  
  
```  
DROP WORKLOAD GROUP adhoc;  
GO  
ALTER RESOURCE GOVERNOR RECONFIGURE;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [Regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [ALTER WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/alter-workload-group-transact-sql.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [ALTER RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-pool-transact-sql.md)   
 [DROP RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/drop-resource-pool-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
::: moniker-end
::: moniker range="=azure-sqldw-latest||=sqlallproducts-allversions"

> ||||
> |---|---|---|
> |[SQL Server](drop-workload-group-transact-sql.md?view=sql-server-2017)||[Instancia administrada de<br />SQL Database](drop-workload-group-transact-sql.md?view=azuresqldb-mi-current)||**_\* SQL Data<br />Warehouse \*_** &nbsp;||||

&nbsp;

## <a name="sql-data-warehouse-preview"></a>SQL Data Warehouse (versión preliminar)

Quita un grupo de cargas de trabajo.  Una vez completada la instrucción, la configuración entra en vigor.

 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo a temas") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).

## <a name="syntax"></a>Sintaxis

```
DROP WORKLOAD GROUP group_name  
```

## <a name="arguments"></a>Argumentos

 *group_name*  
 Es el nombre de un grupo de cargas de trabajo definido por el usuario existente.

## <a name="remarks"></a>Notas

No se puede quitar un grupo de cargas de trabajo si existen clasificadores para ese grupo.  Quite los clasificadores antes de quitar el grupo de cargas de trabajo.  Si hay solicitudes activas que usan recursos del grupo de cargas de trabajo que se van a quitar, la instrucción drop workload se bloquea detrás.

## <a name="examples"></a>Ejemplos

Use el siguiente ejemplo de código para determinar qué clasificadores deben quitarse antes de que se pueda quitar el grupo de cargas de trabajo.

```sql
SELECT c.name as classifier_name
      ,'DROP WORKLOAD CLASSIFIER '+c.name as drop_command
  FROM sys.workload_management_workload_classifiers c
  JOIN sys.workload_management_workload_groups g
    ON c.group_name = g.name
  WHERE g.name = 'wgXYZ' --change the filter to the workload being dropped
```

## <a name="permissions"></a>Permisos

Requiere el permiso CONTROL DATABASE

## <a name="see-also"></a>Vea también
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 
::: moniker-end
