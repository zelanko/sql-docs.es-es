---
title: sp_estimate_data_compression_savings (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_estimate_data_compression_savings_TSQL
- sp_estimate_data_compression_savings
dev_langs:
- TSQL
helpviewer_keywords:
- compression [SQL Server], estimating
- sp_estimate_data_compression_savings
ms.assetid: 6f6c7150-e788-45e0-9d08-d6c2f4a33729
caps.latest.revision: 27
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 25798372f2b949446b746164665dbfe6752443d7
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="spestimatedatacompressionsavings-transact-sql"></a>sp_estimate_data_compression_savings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el tamaño actual del objeto solicitado y calcula el tamaño del objeto para el estado de compresión solicitado. La compresión se puede evaluar para tablas enteras o partes de tablas. Esto incluye montones, índices clúster, índices no clúster, vistas indizadas y particiones de tablas y de índices. Los objetos se pueden comprimir utilizando la compresión de fila o de página. Si la tabla, índice o partición ya están comprimidos, puede utilizar este procedimiento para calcular el tamaño de la tabla, del índice o de la partición en caso de que se volviera a comprimir.  
  
> [!NOTE]  
>  Compresión y **sp_estimate_data_compression_savings** no están disponibles en todas las ediciones de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de las características admitidas por las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Características compatibles con las ediciones de SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
 Para calcular el tamaño del objeto, en caso de que se use el valor de compresión solicitado, el procedimiento almacenado prueba el objeto de origen y carga los datos en una tabla e índice equivalentes creados en tempdb. La tabla o índice creados en tempdb se comprimen al valor solicitado y se calcula el ahorro estimado de la compresión.  
  
 Para cambiar el estado de compresión de una tabla, índice o partición, use la [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md) o [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) instrucciones. Para obtener información general acerca de la compresión, vea [compresión de datos](../../relational-databases/data-compression/data-compression.md).  
  
> [!NOTE]  
>  Si se fragmentan los datos existentes, es posible que pueda reducir su tamaño regenerando el índice y sin necesidad de utilizar la compresión. Para los índices, el factor de relleno se aplicará cuando se vuelva a generar el índice. Esto podría aumentar el tamaño del índice.  

 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_estimate_data_compression_savings   
     [ @schema_name = ] 'schema_name'    
   , [ @object_name = ] 'object_name'   
   , [@index_id = ] index_id   
   , [@partition_number = ] partition_number   
   , [@data_compression = ] 'data_compression'   
[;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @schema_name=] '*schema_name*'  
 Es el nombre del esquema de la base de datos que contiene la tabla o vista indizada. *schema_name* es **sysname**. Si *schema_name* es NULL, se utiliza el esquema predeterminado del usuario actual.  
  
 [ @object_name=] '*object_name*'  
 Es el nombre de la tabla o vista indizada en la que está el índice. *object_name* es **sysname**.  
  
 [ @index_id=] '*index_id*'  
 Es el identificador del índice. *index_id* es **int**, y puede tener uno de los siguientes valores: el número de identificación de un índice, NULL o 0 si *object_id* es un montón. Para obtener información de todos los índices de una tabla base o vista, especifique NULL. Si se especifica NULL, también debe especificar NULL para *número_de_partición*.  
  
 [ @partition_number=] '*número_de_partición*'  
 Es el número de partición en el objeto. *número_de_partición* es **int**, y puede tener uno de los siguientes valores: el número de partición de un índice o montón, NULL o 1 para un montón o índice sin particiones.  
  
 Para especificar la partición, también puede especificar el [$partition](../../t-sql/functions/partition-transact-sql.md) función. Para obtener información sobre todas las particiones del objeto propietario, especifique NULL.  
  
 [ @data_compression=] '*data_compression*'  
 Es el tipo de compresión que se va a evaluar. *DATA_COMPRESSION* puede ser uno de los siguientes valores: NONE, ROW o PAGE.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 El siguiente conjunto de resultados se devuelve para proporcionar el tamaño actual y estimado de la tabla, índice o partición.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|object_name|**sysname**|Nombre de la tabla o vista indizada.|  
|schema_name|**sysname**|Esquema de la tabla o vista indizada.|  
|index_id|**int**|Identificador de índice de un índice:<br /><br /> 0 = Montón<br /><br /> 1 = Índice clúster<br /><br /> > 1 = Índice no clúster|  
|partition_number|**int**|Número de partición. Devuelve 1 para una tabla o índice sin particiones.|  
|size_with_current_compression_setting (KB)|**bigint**|Tamaño actual de la tabla, índice o partición solicitados.|  
|size_with_requested_compression_setting (KB)|**bigint**|Tamaño estimado de la tabla, índice o partición que utiliza el valor de compresión solicitado y, si es aplicable, factor de relleno existente, suponiendo que no hay fragmentación.|  
|sample_size_with_current_compression_setting (KB)|**bigint**|Tamaño del ejemplo con la opción de compresión actual. Esto incluye cualquier fragmentación.|  
|sample_size_with_requested_compression_setting (KB)|**bigint**|Tamaño del ejemplo que se crea utilizando el valor de compresión solicitado y, si es aplicable, factor de relleno existente, sin fragmentación.|  
  
## <a name="remarks"></a>Comentarios  
 Utilice sp_estimate_data_compression_savings para estimar el ahorro que se puede obtener al habilitar una tabla o partición para la compresión de fila o de página. Por ejemplo, si el tamaño medio de una fila se puede reducir un 40 por ciento, potencialmente también se puede reducir el tamaño del objeto en un 40 por ciento. Es posible que no consiga ahorrar espacio, ya que depende del factor de relleno y del tamaño de la fila. Por ejemplo, si una fila tiene 8.000 bytes de longitud y reduce su tamaño en un 40 por ciento, solo podrá seguir incluyendo una fila en una página de datos. No se obtiene ningún ahorro.  
  
 Si los resultados de ejecutar sp_estimated_rowsize_reduction_for_vardecimal indican que la tabla crecerá, eso quiere decir que muchas filas de la tabla utilizan prácticamente toda la precisión en los tipos de datos, y la adición de la mínima sobrecarga necesaria para el formato comprimido es mayor que el ahorro obtenido por la compresión. En este caso excepcional, no habilite la compresión.  
  
 Si una tabla está habilitada para compresión, utilice sp_estimate_data_compression_savings para estimar el tamaño medio de la fila si se descomprime la tabla.  
  
 Durante esta operación, se adquiere un bloqueo con intención compartida (IS) en la tabla. Si no se puede obtener un bloqueo (IS), se bloqueará el procedimiento. La tabla se examina bajo el nivel de aislamiento READ COMMITTED.  
  
 Si el valor de compresión solicitado es mismo que el de la compresión actual, el procedimiento almacenado devolverá el tamaño estimado sin la fragmentación de los datos y utilizando el factor de relleno existente.  
  
 Si no existe el identificador de índice o la partición, no se devolverá ningún resultado.  
  
## <a name="permissions"></a>Permissions  
 Es necesario contar con un permiso de tipo SELECT en la tabla.  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 Este procedimiento no se aplica a tablas de almacén de columnas, por lo que no acepta los parámetros de compresión de datos COLUMNSTORE y COLUMNSTORE_ARCHIVE.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se calcula el tamaño de la tabla `Production.WorkOrderRouting` si se comprime mediante la compresión `ROW`.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_estimate_data_compression_savings 'Production', 'WorkOrderRouting', NULL, NULL, 'ROW' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [sys.partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [Procedimientos almacenados del motor de base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Implementación de la compresión Unicode](../../relational-databases/data-compression/unicode-compression-implementation.md)  
  
  
