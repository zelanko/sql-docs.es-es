---
title: Sys.sp_cdc_enable_table (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sp_cdc_enable_table_TSQL
- sp_cdc_enable_table_TSQL
- sys.sp_cdc_enable_table
- sp_cdc_enable_table
dev_langs: TSQL
helpviewer_keywords:
- change data capture [SQL Server], enabling tables
- sys.sp_cdc_enable_table
- sp_cdc_enable_table
ms.assetid: 26150c09-2dca-46ad-bb01-3cb3165bcc5d
caps.latest.revision: "42"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ef89a0a2bb0689e935558849c4e07bae4251befd
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="sysspcdcenabletable-transact-sql"></a>sys.sp_cdc_enable_table (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Habilita la captura de datos modificados para la tabla de origen especificada en la base de datos actual. Cuando una tabla está habilitada para la captura de datos modificados, un registro de cada operación del lenguaje de manipulación de datos (DML) aplicada a la tabla se escribe en el registro de transacciones. El proceso de captura de datos de cambio recupera esta información del registro y la escribe para cambiar las tablas a las que se accede mediante un conjunto de funciones.  
  
 La captura de datos modificados no está disponible en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sys.sp_cdc_enable_table   
  [ @source_schema = ] 'source_schema',   
  [ @source_name = ] 'source_name' ,  [,[ @capture_instance = ] 'capture_instance' ]  
  [,[ @supports_net_changes = ] supports_net_changes ]  
  , [ @role_name = ] 'role_name'  
  [,[ @index_name = ] 'index_name' ]  
  [,[ @captured_column_list = ] 'captured_column_list' ]  
  [,[ @filegroup_name = ] 'filegroup_name' ]  
  [,[ @allow_partition_switch = ] 'allow_partition_switch' ]  
  [;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@source_schema =** ] **'***source_schema***'**  
 Es el nombre del esquema al que pertenece la tabla de origen. *source_schema* es **sysname**, no tiene ningún valor predeterminado, y no puede ser NULL.  
  
 [  **@source_name =** ] **'***source_name***'**  
 Es el nombre de la tabla de origen en la que se habilita la captura de datos de cambio. *source_name* es **sysname**, no tiene ningún valor predeterminado, y no puede ser NULL.  
  
 *source_name* debe existir en la base de datos actual. Las tablas de la **cdc** esquema no se puede habilitar para la captura de datos modificados.  
  
 [  **@role_name =** ] **'***role_name***'**  
 Es el nombre del rol de base de datos usado para obtener acceso a los datos de cambio. *role_name* es **sysname** y deben especificarse. Si se establece explícitamente en NULL, no se utiliza ningún rol de acceso para limitar el acceso a los datos modificados.  
  
 Se utiliza el rol si ya existe. Si el rol no existe, se intenta crear un rol de base de datos con el nombre especificado. Antes de intentar crear el rol, se recortan los espacios en blanco a la derecha de la cadena del nombre del rol. Si el autor de la llamada no está autorizado a crear un rol dentro de la base de datos, se producirá un error en la operación del procedimiento almacenado.  
  
 [  **@capture_instance =** ] **'***capture_instance***'**  
 Es el nombre de la instancia de captura que se usa para denominar los objetos de captura de datos de cambio específicos de una instancia. *capture_instance* es **sysname** y no puede ser NULL.  
  
 Si no se especifica, el nombre se deriva del nombre de esquema de origen más el nombre de la tabla de origen en el formato *schemaname_sourcename*. *capture_instance* no puede superar los 100 caracteres y debe ser único dentro de la base de datos. Si especificado o derivado, *capture_instance* se recortan los espacios en blanco a la derecha de la cadena.  
  
 Una tabla de origen puede tener un máximo de dos instancias de captura. Para obtener más información, vea [sys.sp_cdc_help_change_data_capture &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md).  
  
 [  **@supports_net_changes =** ] *supports_net_changes*  
 Indica si se permiten las consultas de cambios netos para esta instancia de captura. *supports_net_changes* es **bits** con un valor predeterminado es 1 si la tabla tiene una clave principal o la tabla tiene un índice único que se ha identificado mediante el uso de la @index_name parámetro. De lo contrario, el parámetro tiene como valor predeterminado 0.  
  
 Si es 0, solo se generan las funciones de compatibilidad para consultar todos los cambios.  
  
 Si es 1, se generan también las funciones necesarias para consultar los cambios de la red.  
  
 Si *supports_net_changes* está establecido en 1, *index_name* debe especificarse, o la tabla de origen debe tener definida una clave principal.  
  
 [  **@index_name =** ] **'***index_name*'  
 Nombre de un índice único que se va a usar para identificar de manera inequívoca las filas de la tabla de origen. *index_name* es **sysname** y puede ser NULL. Si se especifica, *index_name* debe ser un índice único válido en la tabla de origen. Si *index_name* se especifica, las columnas de índice identificadas tiene prioridad sobre las columnas de clave principales definidas como el identificador de fila único para la tabla.  
  
 [  **@captured_column_list =** ] **'***captured_column_list***'**  
 Identifica las columnas de la tabla de origen que se incluirán en la tabla de cambios. *captured_column_list* es **nvarchar (max)** y puede ser NULL. Si es NULL, se incluyen todas las columnas en la tabla de cambios.  
  
 Los nombres de columna deben ser columnas válidas de la tabla de origen. Las columnas definidas en un índice de clave principal o columnas definidas en un índice al que hace referencia *index_name* se deben incluir.  
  
 *captured_column_list* es una lista separada por comas de nombres de columna. Los nombres de las columnas individuales que figuran en la lista se pueden incluir opcionalmente entre comillas dobles ("") o corchetes ([]). Si un nombre de columna contiene una coma, se debe entrecomillar el nombre de columna.  
  
 *captured_column_list* no puede contener los siguientes nombres de columna reservados: **__ $start_lsn**, **__ $end_lsn**, **__ $seqval**, **__ $operation**, y **__ $update_mask**.  
  
 [  **@filegroup_name =** ] **'***filegroup_name***'**  
 Es el grupo de archivos que se va a usar en la tabla de cambios creada para la instancia de captura. *filegroup_name* es **sysname** y puede ser NULL. Si se especifica, *filegroup_name* debe estar definida para la base de datos actual. Si es NULL, se usa el grupo de archivos predeterminado.  
  
 Se recomienda crear un grupo de archivos independiente para las tablas de cambios de la captura de datos modificados.  
  
 [  **@allow_partition_switch=** ] **'***allow_partition_switch***'**  
 Indica si el comando SWITCH PARTITION de ALTER TABLE se puede ejecutar en una tabla que esté habilitada para la captura de datos de cambio. *allow_partition_switch* es **bits**, su valor predeterminado es 1.  
  
 Para las tablas sin particiones, el valor del modificador es siempre 1 y se omite el valor real. Si el modificador está establecido explícitamente en 0 para una tabla sin particiones, se genera la advertencia 22857 para indicar que se ha omitido el valor del modificador. Si el modificador está establecido explícitamente en 0 para una tabla con particiones, se genera la advertencia 22356 para indicar que se denegarán las operaciones de modificador de partición en la tabla de origen. Por último, si el valor del modificador está establecido explícitamente en 1 o permite tener como valor predeterminado 1 y la tabla habilitada tiene particiones, se genera la advertencia 22855 para indicar que los modificadores de partición no se bloquearán. Si se realiza alguna operación de modificador de partición, la captura de datos modificados no realizará el seguimiento de los cambios resultantes de dicha operación. Esto producirá incoherencia en los datos cuando se utilicen los datos modificados.  
  
> [!IMPORTANT]  
>  SWITCH PARTITION es una operación de metadatos, pero produce cambios en los datos. Los cambios en los datos asociados a esta operación no se capturan en las tablas de cambios de capturas de datos modificados. Considere una tabla que tiene tres particiones. Se realizan cambios en esta tabla. El proceso de captura realizará el seguimiento de las operaciones de inserción, actualización y eliminación del usuario que se ejecutan en la tabla. Sin embargo, si se desactiva una partición en otra tabla (por ejemplo, para realizar una eliminación masiva), las filas movidas como parte de esta operación no se capturarán como filas eliminadas en la tabla de cambios. De igual forma, si una partición nueva que tiene las filas rellenas de antemano se agrega a la tabla, estas filas no se reflejarán en la tabla de cambios. Esto puede producir incoherencias en los datos cuando una aplicación utilice los cambios y los aplique en el destino.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  
  
## <a name="remarks"></a>Comentarios  
 Para poder habilitar una tabla para la captura de datos modificados, la base de datos debe estar habilitada. Para determinar si la base de datos está habilitada para la captura de datos modificados, consulte el **is_cdc_enabled** columna en el [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) vista de catálogo. Para habilitar la base de datos, use la [sys.sp_cdc_enable_db](../../relational-databases/system-stored-procedures/sys-sp-cdc-enable-db-transact-sql.md) procedimiento almacenado.  
  
 Cuando la captura de datos modificados está habilitada para una tabla, se generan una tabla de cambios y una o dos funciones de consulta. La tabla de cambios actúa de repositorio para los cambios de la tabla de origen extraídos del registro de transacciones por el proceso de captura. Las funciones de consulta se utilizan para extraer los datos de la tabla de cambios. Los nombres de estas funciones se derivan los *capture_instance* parámetro de las maneras siguientes:  
  
-   Todas las funciones de cambios: **cdc.fn_cdc_get_all_changes_ < capture_instance >**  
  
-   Función de cambios netos: **cdc.fn_cdc_get_net_changes_ < capture_instance >**  
  
 **Sys.sp_cdc_enable_table** crea también los trabajos de captura y la limpieza de la base de datos si la tabla de origen es la primera tabla de la base de datos esté habilitado para la captura de datos modificados y no existe ninguna publicación transaccional para la base de datos. Establece el **is_tracked_by_cdc** columna en el [sys.tables](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md) vista en 1 de catálogo.  
  
> [!NOTE]  
>  No es necesario que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se esté ejecutando cuando se habilita la captura de datos modificados para una tabla. Sin embargo, el proceso de captura no procesará las entradas de escritura y del registro de transacciones en la tabla de cambios a menos que se ejecute el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer a la **db_owner** rol fijo de base de datos.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-enabling-change-data-capture-by-specifying-only-required-parameters"></a>A. Habilitar la captura de datos de cambio especificando solo los parámetros necesarios  
 En el siguiente ejemplo se habilita la captura de datos modificados para la tabla `HumanResources.Employee`. Solo se especifican los parámetros necesarios.  
  
```  
USE AdventureWorks2012;  
GO  
EXECUTE sys.sp_cdc_enable_table  
    @source_schema = N'HumanResources'  
  , @source_name = N'Employee'  
  , @role_name = N'cdc_Admin';  
GO  
```  
  
### <a name="b-enabling-change-data-capture-by-specifying-additional-optional-parameters"></a>B. Habilitar la captura de datos de cambio especificando parámetros opcionales adicionales  
 En el siguiente ejemplo se habilita la captura de datos modificados para la tabla `HumanResources.Department`. Se especifican todos los parámetros excepto `@allow_partition_switch`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sys.sp_cdc_enable_table  
    @source_schema = N'HumanResources'  
  , @source_name = N'Department'  
  , @role_name = N'cdc_admin'  
  , @capture_instance = N'HR_Department'   
  , @supports_net_changes = 1  
  , @index_name = N'AK_Department_Name'   
  , @captured_column_list = N'DepartmentID, Name, GroupName'   
  , @filegroup_name = N'PRIMARY';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Sys.sp_cdc_disable_table &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-table-transact-sql.md)   
 [Sys.sp_cdc_help_change_data_capture &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-change-data-capture-transact-sql.md)   
 [CDC.fn_cdc_get_all_changes_ &#60; capture_instance &#62;  &#40; Transact-SQL &#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-all-changes-capture-instance-transact-sql.md)   
 [CDC.fn_cdc_get_net_changes_ &#60; capture_instance &#62; &#40; Transact-SQL &#41;](../../relational-databases/system-functions/cdc-fn-cdc-get-net-changes-capture-instance-transact-sql.md)   
 [Sys.sp_cdc_help_jobs &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sys-sp-cdc-help-jobs-transact-sql.md)  
  
  
