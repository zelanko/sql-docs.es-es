---
title: sp_settriggerorder (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_settriggerorder
- sp_settriggerorder_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_settriggerorder
ms.assetid: 8b75c906-7315-486c-bc59-293ef12078e8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: acbdb4b406d3ec0c2820e2be7988c32af249379c
ms.sourcegitcommit: 37310da0565c2792aae43b3855bd3948fd13e044
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/18/2018
ms.locfileid: "53590319"
---
# <a name="spsettriggerorder-transact-sql"></a>sp_settriggerorder (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Especifica los desencadenadores AFTER que se activan en primer o último lugar. Los desencadenadores AFTER que se activan entre el primero y el último se ejecutan en un orden indefinido.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_settriggerorder [ @triggername = ] '[ triggerschema. ] triggername'   
    , [ @order = ] 'value'   
    , [ @stmttype = ] 'statement_type'   
    [ , [ @namespace = ] { 'DATABASE' | 'SERVER' | NULL } ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@triggername=** ] **'**[ _triggerschema_**.**] _triggername_**'**  
 Es el nombre del desencadenador y el esquema al que pertenece, si procede, cuyo orden se va a establecer o cambiar. [_triggerschema_**.**] *triggername* es **sysname**. Si el nombre no corresponde a un desencadenador o si corresponde a un desencadenador INSTEAD OF, el procedimiento devolverá un error. *triggerschema* no se puede especificar para desencadenadores DDL o logon.  
  
 [ **@order=** ] **'**_valor_**'**  
 Es el valor del nuevo orden del desencadenador. *valor* es **varchar (10)** y puede ser uno de los siguientes valores.  
  
> [!IMPORTANT]  
>  El **primera** y **última** desencadenadores deben ser dos desencadenadores diferentes.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Primero**|El desencadenador se activa primero.|  
|**Último**|El desencadenador se activa el último.|  
|**Ninguno**|El desencadenador se activa sin un orden definido.|  
  
 [  **@stmttype=** ] **'**_statement_type_**'**  
 Especifica la instrucción SQL que activa el desencadenador. *statement_type* es **varchar (50)** y puede ser INSERT, UPDATE, DELETE, LOGON o cualquier [!INCLUDE[tsql](../../includes/tsql-md.md)] enumerado en el evento de instrucción [eventos DDL](../../relational-databases/triggers/ddl-events.md). Los grupos de eventos no se pueden especificar.  
  
 Un desencadenador puede designarse como el **primera** o **última** desencadenador para un tipo de instrucción solo después de haber definido ese desencadenador como desencadenador para ese tipo de instrucción. Por ejemplo, desencadenar **TR1** puede designarse **primera** para INSERT en la tabla **T1** si **TR1** se define como un desencadenador INSERT. El [!INCLUDE[ssDE](../../includes/ssde-md.md)] devuelve un error si **TR1**, que se ha definido solo como un desencadenador INSERT, se establece como un **primera**, o **última**, desencadenador de una instrucción UPDATE. Para obtener más información, vea la sección Comentarios.  
  
 **@namespace=** { **'DATABASE'** | **'SERVER'** | NULL}  
 Cuando *triggername* es un desencadenador DDL, **@namespace** especifica si *triggername* se creó con ámbito de base de datos o de servidor. Si *triggername* es un desencadenador de inicio de sesión, se debe especificar el servidor. Para obtener más información sobre el ámbito del desencadenador DDL, vea [desencadenadores DDL](../../relational-databases/triggers/ddl-triggers.md). Si no se especifica, o si se especifica NULL, *triggername* es un desencadenador DML.  
  
||  
|-|  
|SERVER se aplica a: [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) y 1 (error)  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="dml-triggers"></a>Desencadenadores DML  
 Puede haber solo un **primera** y uno **última** desencadenador para cada instrucción en una sola tabla.  
  
 Si un **primera** desencadenador ya está definido en la tabla, la base de datos o el servidor, no puede designar un nuevo desencadenador como **primera** para la misma tabla, base de datos o servidor para el mismo *statement_type* . También se aplica esta restricción **última** desencadenadores.  
  
 La replicación genera automáticamente un primer desencadenador para cualquier tabla incluida en una suscripción de actualización inmediata o en cola. La replicación requiere que su desencadenador sea el primero. Generará un error si se intenta incluir una tabla con un primer desencadenador en una suscripción de actualización inmediata o en cola. Si intenta convertir un desencadenador en el primero después de haber incluido una tabla en una suscripción, **sp_settriggerorder** devolverá un error. Si utiliza ALTER TRIGGER en el desencadenador de replicación o use **sp_settriggerorder** para cambiar el desencadenador de replicación a un **última** o **ninguno** does de desencadenador, la suscripción no funcione correctamente.  
  
## <a name="ddl-triggers"></a>Desencadenadores DDL  
 Si un desencadenador DDL con ámbito de base de datos y un desencadenador DDL con ámbito en el servidor existen en el mismo evento, puede especificar que ambos desencadenadores sean un **primera** desencadenador o una **última** desencadenador. Sin embargo, los desencadenadores con ámbito de servidor siempre se inician en primer lugar. En general, el orden de ejecución de los desencadenadores DDL que existen en el mismo evento es el siguiente:  
  
1.  El desencadenador de nivel de servidor marcado **primera**.  
  
2.  Otros desencadenadores de servidor.  
  
3.  El desencadenador de nivel de servidor marcado **última**.  
  
4.  El desencadenador de nivel de base de datos marcado **primera**.  
  
5.  Otros desencadenadores de base de datos.  
  
6.  El desencadenador de nivel de base de datos marcado **última**.  
  
## <a name="general-trigger-considerations"></a>Consideraciones generales sobre los desencadenadores  
 Si una instrucción ALTER TRIGGER cambia un desencadenador primero o último, el **primera** o **última** se quita el atributo establecido originalmente en el desencadenador y el valor se sustituye por **ninguno**. El valor de orden se debe restablecer mediante **sp_settriggerorder**.  
  
 Si el mismo desencadenador debe designarse como el orden primero o último para más de un tipo de instrucción, **sp_settriggerorder** se debe ejecutar para cada tipo de instrucción. Además, el desencadenador debe primero definirse para un tipo de instrucción antes de se puede designar como el **primera** o **última** desencadenador para ese tipo de instrucción.  
  
## <a name="permissions"></a>Permisos  
 Para establecer el orden de un desencadenador DDL con ámbito de servidor (ON ALL SERVER) o de un desencadenador de inicio de sesión se requiere el permiso CONTROL SERVER.  
  
 Para establecer el orden de un desencadenador DDL con ámbito de base de datos (ON DATABASE), se necesita el permiso ALTER ANY DATABASE DDL TRIGGER.  
  
 Para establecer el orden de un desencadenador DML, se necesita el permiso ALTER para la tabla o la vista donde está definido el desencadenador.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-setting-the-firing-order-for-a-dml-trigger"></a>A. Configurar el orden de activación de un desencadenador DML  
 En el siguiente ejemplo se especifica que `uSalesOrderHeader` sea el primer desencadenador que se active después de que se produzca una operación `UPDATE` en la tabla `Sales.SalesOrderHeader`.  
  
```  
USE AdventureWorks2012;  
GO  
sp_settriggerorder @triggername= 'Sales.uSalesOrderHeader', @order='First', @stmttype = 'UPDATE';  
```  
  
### <a name="b-setting-the-firing-order-for-a-ddl-trigger"></a>b. Configurar el orden de activación de un desencadenador DDL  
 El siguiente ejemplo especifica que `ddlDatabaseTriggerLog` sea el primer desencadenador que se active después de que se produzca un evento `ALTER_TABLE` en la tabla [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
USE AdventureWorks2012;  
GO  
sp_settriggerorder @triggername= 'ddlDatabaseTriggerLog', @order='First', @stmttype = 'ALTER_TABLE', @namespace = 'DATABASE';  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimientos almacenados del motor de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)  
  
  
