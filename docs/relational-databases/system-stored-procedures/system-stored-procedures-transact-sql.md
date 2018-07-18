---
title: (Transact-SQL) de procedimientos almacenados del sistema | Microsoft Docs
ms.custom: ''
ms.date: 02/21/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server (starting with 2016 CTP3)
f1_keywords:
- sql13.TSQLSysNoExpandPortal.f1
- sql13.TSQLSysNoExpandPortal.f1_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- stored procedures [SQL Server]
- APIs [SQL Server]
- stored procedures [SQL Server], categories
- system stored procedures [SQL Server], categories
- system stored procedures [SQL Server]
ms.assetid: a5c4d5b8-5a24-4a2d-99b4-d003b546ee3a
caps.latest.revision: 49
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 481b0c451f5161231cf64402c5c758870a07be62
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37979467"
---
# <a name="system-stored-procedures-transact-sql"></a>Procedimientos almacenados del sistema (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], muchas actividades administrativas e informativas se pueden realizar mediante los procedimientos almacenados del sistema. Los procedimientos almacenados del sistema se agrupan en las categorías que aparecen en la siguiente tabla.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Categoría|Descripción|  
|--------------|-----------------|  
|[Procedimientos almacenados de replicación geográfica activa](http://msdn.microsoft.com/library/81658ee4-4422-4d73-bf7a-86a07422cb0d)|Utilizado para administrar las configuraciones de replicación geográfica activa en Azure SQL Database|  
|[Procedimientos almacenados del catálogo](../../relational-databases/system-stored-procedures/catalog-stored-procedures-transact-sql.md)|Se utilizan para implementar las funciones del diccionario de datos ODBC y aislar las aplicaciones ODBC de los cambios en las tablas subyacentes del sistema.|  
|[Procedimientos almacenados de captura de datos modificados](../../relational-databases/system-stored-procedures/change-data-capture-stored-procedures-transact-sql.md)|Permiten habilitar, deshabilitar o informar sobre los objetos de la captura de datos modificados.|  
|[Procedimientos almacenados de cursor](../../relational-databases/system-stored-procedures/cursor-stored-procedures-transact-sql.md)|Se utilizan para implementar la funcionalidad de variable de cursor.|  
|[Procedimientos almacenados del recopilador de datos](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)|Se utiliza para trabajar con el recopilador de datos y los componentes siguientes: conjuntos de recopilación, elementos de recopilación y tipos de recopilación.|  
|[Procedimientos almacenados del motor de base de datos](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)|Se utilizan para el mantenimiento general de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].|  
|[Procedimientos almacenados de correo electrónico de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-mail-stored-procedures-transact-sql.md)|Se utilizan para realizar operaciones de correo electrónico desde una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Procedimientos almacenados de planes de mantenimiento de base de datos](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)|Se utilizan para configurar las tareas de mantenimiento fundamentales necesarias para administrar el rendimiento de las bases de datos.|  
|[Procedimientos almacenados de consultas distribuidas](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)|Se utilizan para implementar y administrar consultas distribuidas.|  
|[FileStream y procedimientos almacenados de FileTable &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/54beca08-c012-4ebd-aa68-d8a10d221b64)|Se usa para configurar y administrar las características FILESTREAM y FileTable.|  
|[Procedimientos almacenan de reglas de Firewall &#40;base de datos SQL Azure&#41;](../../relational-databases/system-stored-procedures/firewall-rules-stored-procedures-azure-sql-database.md)|Se usa para configurar el firewall de Azure SQL Database.|  
|[Procedimientos almacenados de búsqueda de texto completo](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)|Se utilizan para implementar y consultar índices de texto completo.|  
|[Procedimientos almacenados extendidos generales](../../relational-databases/system-stored-procedures/general-extended-stored-procedures-transact-sql.md)|Proporcionan una interfaz de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a los programas externos para diversas actividades de mantenimiento.|  
|[Trasvase de registros de procedimientos almacenados](../../relational-databases/system-stored-procedures/log-shipping-stored-procedures-transact-sql.md)|Se utilizan para establecer, modificar y supervisar las configuraciones de trasvase de registros.|  
|[Procedimientos almacenados de almacén de datos de administración &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/management-data-warehouse-stored-procedures-transact-sql.md)|Se usa para configurar el almacén de datos de administración.|  
|[OLE Automation procedimientos almacenados](../../relational-databases/system-stored-procedures/ole-automation-stored-procedures-transact-sql.md)|Permiten habilitar el uso de objetos de Automation estándar en un lote estándar de [!INCLUDE[tsql](../../includes/tsql-md.md)].|  
|[Procedimientos almacenados de administración basada en directivas](../../relational-databases/system-stored-procedures/policy-based-management-stored-procedures-transact-sql.md)|Se usan para la administración basada en directivas.|  
|[Procedimientos almacenados de PolyBase](http://msdn.microsoft.com/library/a522b303-bd1b-410b-92d1-29c950a15ede)|Agregar o quitar un equipo de un grupo de escalabilidad horizontal de PolyBase.|  
|[Procedimientos almacenados de Query Store &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql.md)|Se utiliza para optimizar el rendimiento.|  
|[Procedimientos almacenados de replicación](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)|Se utilizan para administrar la replicación.|  
|[Procedimientos almacenados de seguridad](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)|Se utilizan para administrar la seguridad.|  
|[Procedimientos almacenados de copia de seguridad de instantánea](http://msdn.microsoft.com/library/c278db87-5770-4037-a1e6-b9853a943339)|Se usa para eliminar la copia de seguridad FILE_SNAPSHOT junto con todas sus instantáneas o eliminar una instantánea de archivos de copia de seguridad individuales.|  
|[Procedimientos almacenados de índice espacial](http://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)|Se utiliza para analizar y mejorar el rendimiento de la indización de los índices espaciales.|  
|[Procedimientos almacenados del Agente SQL Server](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)|Lo utiliza [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para supervisar el rendimiento y la actividad.|  
|[Procedimientos almacenados de SQL Server Profiler](../../relational-databases/system-stored-procedures/sql-server-profiler-stored-procedures-transact-sql.md)|Los utiliza el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para administrar actividades programadas y controladas por eventos.|  
|[Stretch Database almacena los procedimientos](../../relational-databases/system-stored-procedures/stretch-database-extended-stored-procedures-transact-sql.md)|Se usa para administrar bases de datos de stretch.|  
|[Procedimientos almacenados de tablas temporales](http://msdn.microsoft.com/library/f28ca74e-7876-4592-b794-e78e3690fff6)|Uso de las tablas temporales|  
|[Procedimientos almacenados de XML](../../relational-databases/system-stored-procedures/xml-stored-procedures-transact-sql.md)|Se utilizan para la administración del texto XML.|  
  
> [!NOTE]  
>  A menos que se documente específicamente lo contrario, todos los procedimientos almacenados del sistema devuelven el valor 0 para indicar que son correctos. Para indicar un error, se devuelve un valor distinto de cero.  
  
## <a name="api-system-stored-procedures"></a>Procedimientos almacenados del sistema de la API  
 Los usuarios que ejecutan [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] con aplicaciones ADO, OLE DB y ODBC pueden observar que dichas aplicaciones usan procedimientos almacenados del sistema que no se tratan en la Referencia de [!INCLUDE[tsql](../../includes/tsql-md.md)]. Estos procedimientos almacenados se utilizan por el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB y la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client para implementar la funcionalidad de una API de base de datos. Estos procedimientos almacenados simplemente son el mecanismo que el proveedor o el controlador utiliza para comunicar las solicitudes del usuario a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Están destinados al uso interno del proveedor o el controlador. Llamarlos explícitamente desde una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-no se admite la aplicación basada en.  
  
 El almacenados sp_createorphan y sp_droporphans se utilizan procedimientos para ODBC **ntext**, **texto**, y **imagen** de procesamiento.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza el procedimiento almacenado sp_reset_connection para permitir las llamadas a procedimientos almacenados remotos en una transacción. Este procedimiento almacenado también hace que se activen los eventos Audit Login y Audit Logout cuando se reutiliza una conexión de un grupo de conexiones.  
  
 Los procedimientos almacenados del sistema de las siguientes tablas solo se utilizan en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o a través de las API cliente y no están destinados al uso general. Están sujetos a cambios y su compatibilidad no está garantizada.  
  
 Los siguientes procedimientos almacenados están documentados en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
|||  
|-|-|  
|sp_catalogs|sp_column_privileges|  
|sp_column_privileges_ex|sp_columns|  
|sp_columns_ex|sp_databases|  
|sp_cursor|sp_cursorclose|  
|sp_cursorexecute|sp_cursorfetch|  
|sp_cursoroption|sp_cursoropen|  
|sp_cursorprepare|sp_cursorprepexec|  
|sp_cursorunprepare|sp_execute|  
|sp_datatype_info|sp_fkeys|  
|sp_foreignkeys|sp_indexes|  
|sp_pkeys|sp_primarykeys|  
|sp_prepare|sp_prepexec|  
|sp_prepexecrpc|sp_unprepare|  
|sp_server_info|sp_special_columns|  
|sp_sproc_columns|sp_statistics|  
|sp_table_privileges|sp_table_privileges_ex|  
|sp_tables|sp_tables_ex|  
  
 Los siguientes procedimientos almacenados no están documentados:  
  
|||  
|-|-|  
|sp_assemblies_rowset|sp_assemblies_rowset_rmt|  
|sp_assemblies_rowset2|sp_assembly_dependencies_rowset|  
|sp_assembly_dependencies_rowset_rmt|sp_assembly_dependencies_rowset2|  
|sp_bcp_dbcmptlevel|sp_catalogs_rowset|  
|sp_catalogs_rowset;2|sp_catalogs_rowset;5|  
|sp_catalogs_rowset_rmt|sp_catalogs_rowset2|  
|sp_check_constbytable_rowset|sp_check_constbytable_rowset;2|  
|sp_check_constbytable_rowset2|sp_check_constraints_rowset|  
|sp_check_constraints_rowset;2|sp_check_constraints_rowset2|  
|sp_column_privileges_rowset|sp_column_privileges_rowset;2|  
|sp_column_privileges_rowset;5|sp_column_privileges_rowset_rmt|  
|sp_column_privileges_rowset2|sp_columns_90|  
|sp_columns_90_rowset|sp_columns_90_rowset_rmt|  
|sp_columns_90_rowset2|sp_columns_ex_90|  
|sp_columns_rowset|sp_columns_rowset;2|  
|sp_columns_rowset;5|sp_columns_rowset_rmt|  
|sp_columns_rowset2|sp_constr_col_usage_rowset|  
|sp_datatype_info_90|sp_ddopen;1|  
|sp_ddopen;10|sp_ddopen;11|  
|sp_ddopen;12|sp_ddopen;13|  
|sp_ddopen;2|sp_ddopen;3|  
|sp_ddopen;4|sp_ddopen;5|  
|sp_ddopen;6|sp_ddopen;7|  
|sp_ddopen;8|sp_ddopen;9|  
|sp_foreign_keys_rowset|sp_foreign_keys_rowset;2|  
|sp_foreign_keys_rowset;3|sp_foreign_keys_rowset;5|  
|sp_foreign_keys_rowset_rmt|sp_foreign_keys_rowset2|  
|sp_foreign_keys_rowset3|sp_indexes_90_rowset|  
|sp_indexes_90_rowset_rmt|sp_indexes_90_rowset2|  
|sp_indexes_rowset|sp_indexes_rowset;2|  
|sp_indexes_rowset;5|sp_indexes_rowset_rmt|  
|sp_indexes_rowset2|sp_linkedservers_rowset|  
|sp_linkedservers_rowset;2|sp_linkedservers_rowset2|  
|sp_oledb_database|sp_oledb_defdb|  
|sp_oledb_deflang|sp_oledb_language|  
|sp_oledb_ro_usrname|sp_primary_keys_rowset|  
|sp_primary_keys_rowset;2|sp_primary_keys_rowset;3|  
|sp_primary_keys_rowset;5|sp_primary_keys_rowset_rmt|  
|sp_primary_keys_rowset2|sp_procedure_params_90_rowset|  
|sp_procedure_params_90_rowset2|sp_procedure_params_rowset|  
|sp_procedure_params_rowset;2|sp_procedure_params_rowset2|  
|sp_procedures_rowset|sp_procedures_rowset;2|  
|sp_procedures_rowset2|sp_provider_types_90_rowset|  
|sp_provider_types_rowset|sp_schemata_rowset|  
|sp_schemata_rowset;3|sp_special_columns_90|  
|sp_sproc_columns_90|sp_statistics_rowset|  
|sp_statistics_rowset;2|sp_statistics_rowset2|  
|sp_stored_procedures|sp_table_constraints_rowset|  
|sp_table_constraints_rowset;2|sp_table_constraints_rowset2|  
|sp_table_privileges_rowset|sp_table_privileges_rowset;2|  
|sp_table_privileges_rowset;5|sp_table_privileges_rowset_rmt|  
|sp_table_privileges_rowset2|sp_table_statistics_rowset|  
|sp_table_statistics_rowset;2|sp_table_statistics2_rowset|  
|sp_tablecollations|sp_tablecollations_90|  
|sp_tables_info_90_rowset|sp_tables_info_90_rowset_64|  
|sp_tables_info_90_rowset2|sp_tables_info_90_rowset2_64|  
|sp_tables_info_rowset|sp_tables_info_rowset;2|  
|sp_tables_info_rowset_64|sp_tables_info_rowset_64;2|  
|sp_tables_info_rowset2|sp_tables_info_rowset2_64|  
|sp_tables_rowset;2|sp_tables_rowset;5|  
|sp_tables_rowset_rmt|sp_tables_rowset2|  
|sp_usertypes_rowset|sp_usertypes_rowset_rmt|  
|sp_usertypes_rowset2|sp_views_rowset|  
|sp_views_rowset2|sp_xml_schema_rowset|  
|sp_xml_schema_rowset2||  
  
## <a name="see-also"></a>Vea también  
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [Procedimientos almacenados &#40;motor de base de datos&#41;](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)   
 [Ejecutar procedimientos almacenados &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/stored-procedures-running.md)   
 [Ejecutar procedimientos almacenados](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)   
 [Procedimientos almacenados del motor de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Ejecutar procedimientos almacenados](../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)  
  
  
