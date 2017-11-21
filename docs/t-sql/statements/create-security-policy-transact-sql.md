---
title: Crear directiva de seguridad (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SECURITY_POLICY_TSQL
- CREATE SECURITY
- SECURITY
- CREATE_SECURITY_POLICY_TSQL
- CREATE_SECURITY_TSQL
- SECURITY POLICY
- SECURITY_TSQL
- CREATE SECURITY POLICY
dev_langs:
- TSQL
helpviewer_keywords:
- RLS
- CREATE SECURITY POLICY statement
- Row-Level Security
ms.assetid: d6ab70ee-0fa2-469c-96f6-a3c16d673bc8
caps.latest.revision: 18
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 53292dc3f9f5cbd36913276496084d4648f13520
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-security-policy-transact-sql"></a>Crear directiva de seguridad (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Crea una directiva de seguridad para la seguridad de nivel de fila.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```     
CREATE SECURITY POLICY [schema_name. ] security_policy_name    
    { ADD [ FILTER | BLOCK ] } PREDICATE tvf_schema_name.security_predicate_function_name   
      ( { column_name | arguments } [ , …n] ) ON table_schema_name. table_name    
      [ <block_dml_operation> ] , [ , …n] 
    [ WITH ( STATE = { ON | OFF }  [,] [ SCHEMABINDING = { ON | OFF } ] ) ]  
    [ NOT FOR REPLICATION ] 
[;]  
  
<block_dml_operation>  
    [ { AFTER { INSERT | UPDATE } }   
    | { BEFORE { UPDATE | DELETE } } ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *security_policy_name*  
 El nombre de la directiva de seguridad. Los nombres de directivas de seguridad deben seguir las reglas de los identificadores y deben ser únicos en la base de datos y para su esquema.  
  
 *schema_name*  
 Es el nombre del esquema al que pertenece la directiva de seguridad. *schema_name* es necesaria debido a los enlaces de esquema.  
  
 [FILTRO | BLOQUE]  
 El tipo de predicado de seguridad de la función que se enlaza a la tabla de destino. Los predicados de filtro filtran en modo silencioso las filas que están disponibles para las operaciones de lectura. BLOQUE predicados explícitamente que las operaciones de escritura de bloque que infringen la función de predicado.  
  
 *tvf_schema_name.security_predicate_function_name*  
 Es la función de valor de tabla insertada que se usará como predicado y que se aplicará en las consultas en una tabla de destino. Se puede definir, como máximo, un predicado de seguridad para una operación DML determinada en una tabla determinada. La función de valor de tabla insertada se debe haber creado con la opción SCHEMABINDING.  
  
 { *column_name* | *argumentos* }  
 El nombre de columna o la expresión que se usan como parámetros de la función de predicado de seguridad. Todas las columnas de la tabla de destino pueden utilizarse como argumentos de la función de predicado. Pueden utilizarse expresiones que incluyen literales, builtins y expresiones que usan operadores aritméticos.  
  
 *table_schema_name.table_name*  
 Es la tabla de destino a la que se aplicará el predicado de seguridad. Varias directivas de seguridad deshabilitado pueden tener como destino una sola tabla para una operación DML determinada, pero sólo uno puede habilitarse en un momento dado.  
  
 *\<block_dml_operation >* la operación DML determinada para los que se aplicará el predicado de bloqueo. DESPUÉS, especifica que el predicado se va a evaluar los valores de las filas después de la operación de DML fue realizada (INSERT o UPDATE). Especifica antes que el predicado se va a evaluar los valores de las filas antes de que la operación DML se realizan (UPDATE o DELETE). Si se ha especificado ninguna operación, el predicado se aplicará a todas las operaciones.  
  
 [ESTADO = {ON | **OFF** }]  
 Habilita o deshabilita la aplicación de los predicados de seguridad de la directiva de seguridad en las tablas de destino. Si no se especifica, se habilita la directiva de seguridad que se está creando.  
  
 [SCHEMABINDING = {ON | {OFF}]  
 Indica si se deben crear todas las funciones de predicado de la directiva con la opción SCHEMABINDING. De forma predeterminada, todas las funciones deben crearse con SCHEMABINDING.  
  
 NOT FOR REPLICATION  
 Indica que la directiva de seguridad no debe ejecutarse cuando un agente de replicación modifica el objeto de destino. Para obtener más información, vea [Controlar el comportamiento de desencadenadores y restricciones durante la sincronización &#40;programación de la replicación con Transact-SQL&#41;](../../relational-databases/replication/control-behavior-of-triggers-and-constraints-in-synchronization.md).  
  
 [*table_schema_name*.] *table_name*  
 Es la tabla de destino a la que se aplicará el predicado de seguridad. Puede haber varias directivas de seguridad deshabilitadas que tengan como destino una sola tabla, pero no puede haber varias de ellas habilitadas al mismo tiempo.  
  
## <a name="remarks"></a>Comentarios  
 Al utilizar las funciones de predicado con tablas optimizadas en memoria, debe incluir **SCHEMABINDING** y use la **WITH NATIVE_COMPILATION** sugerencia de compilación.  
  
 Los predicados de bloqueo se evalúan después de ejecuta la operación de DML correspondiente. Por lo tanto, una consulta READ UNCOMMITTED puede ver valores transitorios que se revertirá.  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso ALTER ANY SECURITY POLICY y el permiso ALTER en el esquema.  
  
 Además, son necesarios los siguientes permisos para cada predicado que se agrega:  
  
-   Los permisos SELECT y REFERENCES en la función que se utiliza como predicado.  
  
-   El permiso REFERENCES en la tabla de destino que se enlaza a la directiva.  
  
-   El permiso REFERENCES en todas las columnas de la tabla de destino que se utilizan como argumentos.  
  
## <a name="examples"></a>Ejemplos  
 Los ejemplos siguientes muestran el uso de la sintaxis de **CREATE SECURITY POLICY** . Para obtener un ejemplo de un escenario de directiva de seguridad completa, consulte [seguridad de nivel de fila](../../relational-databases/security/row-level-security.md).  
  
### <a name="a-creating-a-security-policy"></a>A. Creación de una directiva de seguridad  
 La siguiente sintaxis crea una directiva de seguridad con un predicado de filtro para la tabla Customer y deja deshabilitada la directiva de seguridad.  
  
```  
CREATE SECURITY POLICY [FederatedSecurityPolicy]   
ADD FILTER PREDICATE [rls].[fn_securitypredicate]([CustomerId])   
ON [dbo].[Customer];  
```  
  
### <a name="b-creating-a-policy-that-affects-multiple-tables"></a>B. Creación de una directiva que afecta a varias tablas  
 La siguiente sintaxis crea una directiva de seguridad con tres predicados de filtro en tres tablas diferentes y habilita la directiva de seguridad.  
  
```  
CREATE SECURITY POLICY [FederatedSecurityPolicy]   
ADD FILTER PREDICATE [rls].[fn_securitypredicate1]([CustomerId])   
    ON [dbo].[Customer],  
ADD FILTER PREDICATE [rls].[fn_securitypredicate1]([VendorId])   
    ON [dbo].[ Vendor],  
ADD FILTER PREDICATE [rls].[fn_securitypredicate2]([WingId])   
    ON [dbo].[Patient]  
WITH (STATE = ON);  
```  
  
### <a name="c-creating-a-policy-with-multiple-types-of-security-predicates"></a>C. Crear una directiva con varios tipos de predicados de seguridad  
 Agregar un predicado de filtro y un predicado de bloqueo a la tabla Sales.  
  
```  
CREATE SECURITY POLICY rls.SecPol  
    ADD FILTER PREDICATE rls.tenantAccessPredicate(TenantId) ON dbo.Sales,  
    ADD BLOCK PREDICATE rls.tenantAccessPredicate(TenantId) ON dbo.Sales AFTER INSERT;  
```  
  
## <a name="see-also"></a>Vea también  
 [Seguridad de nivel de fila](../../relational-databases/security/row-level-security.md)   
 [ALTER SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/alter-security-policy-transact-sql.md)   
 [DROP SECURITY POLICY &#40;Transact-SQL&#41;](../../t-sql/statements/drop-security-policy-transact-sql.md)   
 [sys.security_policies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)   
 [Sys.security_predicates &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)  
  
  


