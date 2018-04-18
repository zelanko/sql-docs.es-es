---
title: Sys.dm_db_persisted_sku_features (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 08/23/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_persisted_sku_features_TSQL
- sys.dm_db_persisted_sku_features
- dm_db_persisted_sku_features_TSQL
- dm_db_persisted_sku_features
dev_langs:
- TSQL
helpviewer_keywords:
- editions [SQL Server], feature restrictions
- sys.dm_db_persisted_sku_features dynamic management view
ms.assetid: b4b29e97-b523-41b9-9528-6d4e84b89e09
caps.latest.revision: 26
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0cbc96b18346f6e55f4029e795c22557f6107e7b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmdbpersistedskufeatures-transact-sql"></a>sys.dm_db_persisted_sku_features (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Algunas características de la [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] cambiar la manera en que [!INCLUDE[ssDE](../../includes/ssde-md.md)] almacena información en los archivos de base de datos. Estas características están restringidas a ediciones concretas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Una base de datos que contiene estas características no se puede mover a una edición de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que no los admita. Utilice la vista de administración dinámica sys.dm_db_persisted_sku_features para enumerar las características específicas de la edición que estén habilitadas en la base de datos actual.
  
**Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|feature_name|**sysname**|Nombre externo de la característica que está habilitada en la base de datos pero no admitida en todas las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta característica se debe quitar para poder migrar la base de datos a todas las ediciones disponibles de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|feature_id|**int**|Id. de la característica asociado a la característica. [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)].|  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso VIEW DATABASE STATE en la base de datos.  
  
## <a name="remarks"></a>Comentarios  
 Si no hay características que pueden estar restringidas por una edición específica se usan la base de datos, la vista no devuelve ninguna fila.  
  
 Sys.dm_db_persisted_sku_features puede enumerar las siguientes características de cambio de base de datos como restringidas a determinados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ediciones:  
  
-   **ChangeCapture**: indica que una base de datos tiene habilitada la captura de datos de cambio. Para quitar la captura de datos modificados, utilice la [sys.sp_cdc_disable_db](../../relational-databases/system-stored-procedures/sys-sp-cdc-disable-db-transact-sql.md) procedimiento almacenado. Para obtener más información, vea [Acerca de la captura de datos modificados &#40;SQL Server&#41;](../../relational-databases/track-changes/about-change-data-capture-sql-server.md).  
  
-   **ColumnStoreIndex**: indica que al menos una tabla tiene un índice de almacén de columnas. Para habilitar una base de datos se muevan a una edición de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que no admite esta característica, use la [DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md) o [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) instrucción que se va a quitar el índice de almacén de columnas. Para obtener más información, consulte [índices de almacén de columnas](../../relational-databases/indexes/columnstore-indexes-overview.md).  
  
    **Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
-   **Compresión**: indica que al menos una tabla o un índice usa compresión de datos o el formato de almacenamiento vardecimal. Para habilitar una base de datos se muevan a una edición de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que no admite esta característica, use la [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) o [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) instrucción que se va a quitar la compresión de datos. Para quitar el formato de almacenamiento vardecimal, utilice la instrucción sp_tableoption. Para obtener más información, consulte [Data Compression](../../relational-databases/data-compression/data-compression.md).  
  
-   **MultipleFSContainers**: indica que la base de datos utiliza varios contenedores FILESTREAM. La base de datos tiene un grupo de archivos FILESTREAM con varios contenedores (archivos). Para obtener más información, vea [FILESTREAM &#40;SQL Server&#41;](../../relational-databases/blob/filestream-sql-server.md).  
  
-   **InMemoryOLTP**: indica que la base de datos utiliza OLTP en memoria. La base de datos tiene un grupo de archivos MEMORY_OPTIMIZED_DATA. Para obtener más información, vea [OLTP en memoria &#40;optimización en memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md).  
  
  **Se aplica a:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]). 
  
-   **Creación de particiones.** Indica que la base de datos contiene tablas con particiones, índices con particiones, esquemas de partición o funciones de partición. Para poder mover una base de datos a una edición de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que no sea Enterprise o Developer, no basta con modificar la tabla para que esté en una sola partición. Es necesario quitar la tabla con particiones. Si la tabla contiene datos, utilice SWITCH PARTITION para convertir cada partición en una tabla sin particiones. A continuación, elimine la tabla con particiones, el esquema de partición y la función de partición.  
  
-   **TransparentDataEncryption.** Indica que una base de datos se ha cifrado utilizando el cifrado de datos transparente. Para quitar el cifrado de datos transparente, utilice la instrucción ALTER DATABASE. Para obtener más información, vea [Cifrado de datos transparente &#40;TDE&#41;](../../relational-databases/security/encryption/transparent-data-encryption.md).  

> [!NOTE]
> A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] Service Pack 1, estas características están disponibles en varias [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ediciones y sin limitarse únicamente a Enterprise o Developer Edition.

 Para determinar si una base de datos utiliza alguna característica que esté restringida a ediciones concretas, ejecute la instrucción siguiente en la base de datos:  
  
```sql  
SELECT feature_name FROM sys.dm_db_persisted_sku_features;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Vistas de administración dinámica relacionadas con la base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)   
 [Ediciones y características admitidas de SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md)   
 [Ediciones y las características admitidas de SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md)  
  
