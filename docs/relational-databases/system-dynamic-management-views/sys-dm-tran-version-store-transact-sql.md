---
title: Sys.dm_tran_version_store (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/30/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_tran_version_store_TSQL
- sys.dm_tran_version_store
- dm_tran_version_store
- dm_tran_version_store_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_tran_version_store dynamic management view
ms.assetid: 7ab44517-0351-4f91-bdd9-7cf940f03c51
caps.latest.revision: 32
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7de332c09b586b1c3a7feba4097a940ba9f29a83
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2018
ms.locfileid: "34467631"
---
# <a name="sysdmtranversionstore-transact-sql"></a>sys.dm_tran_version_store (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve una tabla virtual que muestra todos los registros de versión del almacén de versiones. **Sys.dm_tran_version_store** es eficaz ejecutar, ya que consulta el almacén de versiones completo y el almacén de versiones puede ser muy grande.  
  
 Cada registro de versión se almacena como datos binarios junto con alguna información de estado o seguimiento. Al igual que los registros en tablas de base de datos, los registros del almacén de versiones se almacenan en páginas de 8.192 bytes. Si un registro supera los 8.192 bytes, se dividirá en dos registros diferentes.  
  
 Puesto que el registro de versiones se almacena como binario, no existen problemas con las diferentes intercalaciones de bases de datos distintas. Use **sys.dm_tran_version_store** para encontrar las versiones anteriores de las filas en representación binaria como existen en el almacén de versiones.  
  
  
## <a name="syntax"></a>Sintaxis  
  
```  
sys.dm_tran_version_store  
```  
  
## <a name="table-returned"></a>Tabla devuelta  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**transaction_sequence_num**|**bigint**|Número de secuencia de la transacción que genera la versión de registro.|  
|**version_sequence_num**|**bigint**|Número de secuencia del registro de versión. Este valor es único en la transacción que genera la versión.|  
|**database_id**|**int**|Id. de la base de datos del registro de versiones.|  
|**rowset_id**|**bigint**|Id. del conjunto de filas del registro.|  
|**status**|**tinyint**|Indica si un registro de versiones se ha dividido en dos registros. Si el valor es 0, el registro está almacenado en una página. Si el valor es 1, el registro está dividido en dos registros almacenados en dos páginas diferentes.|  
|**min_length_in_bytes**|**smallint**|Longitud mínima del registro en bytes.|  
|**record_length_first_part_in_bytes**|**smallint**|Longitud de la primera parte del registro de versiones en bytes.|  
|**record_image_first_part**|**varbinary(8000)**|Imagen binaria de la primera parte del registro de versiones.|  
|**record_length_second_part_in_bytes**|**smallint**|Longitud de la segunda parte del registro de versiones en bytes.|  
|**record_image_second_part**|**varbinary(8000)**|Imagen binaria de la segunda parte del registro de versiones.|  
  
## <a name="permissions"></a>Permissions

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requiere el `VIEW DATABASE STATE` permiso en la base de datos.   
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se utiliza un escenario de prueba con cuatro transacciones simultáneas, identificadas con un número de secuencia de transacción (XSN), que se ejecutan en una base de datos con las opciones ALLOW_SNAPSHOT_ISOLATION y READ_COMMITTED_SNAPSHOT establecidas en ON. Se están ejecutando las siguientes transacciones:  
  
-   XSN-57 es una operación de actualización con aislamiento serializable.  
  
-   XSN-58 es igual que XSN-57.  
  
-   XSN-59 es una operación de selección con aislamiento de instantáneas.  
  
-   XSN-60 es igual que XSN-59.  
  
 Se ejecuta la siguiente consulta.  
  
```  
SELECT  
    transaction_sequence_num,  
    version_sequence_num,  
    database_id rowset_id,  
    status,  
    min_length_in_bytes,  
    record_length_first_part_in_bytes,  
    record_image_first_part,  
    record_length_second_part_in_bytes,  
    record_image_second_part  
  FROM sys.dm_tran_version_store;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
transaction_sequence_num version_sequence_num database_id  
------------------------ -------------------- -----------  
57                      1                    9             
57                      2                    9             
57                      3                    9             
58                      1                    9             
  
rowset_id            status min_length_in_bytes  
-------------------- ------ -------------------  
72057594038321152    0      12                   
72057594038321152    0      12                   
72057594038321152    0      12                   
72057594038386688    0      16                   
  
record_length_first_part_in_bytes  
---------------------------------  
29                                 
29                                 
29                                 
33                                 
  
record_image_first_part                                               
--------------------------------------------------------------------  
0x50000C0073000000010000000200FCB000000001000000270000000000          
0x50000C0073000000020000000200FCB000000001000100270000000000          
0x50000C0073000000030000000200FCB000000001000200270000000000          
0x500010000100000002000000030000000300F800000000000000002E0000000000  
  
record_length_second_part_in_bytes record_image_second_part  
---------------------------------- ------------------------  
0                                  NULL  
0                                  NULL  
0                                  NULL  
0                                  NULL  
```  
  
 En la salida se muestra que XSN-57 ha creado tres versiones de fila de una tabla y que XSN-58 ha creado una versión de fila de otra tabla.  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funciones y vistas de administración dinámica relacionadas con transacciones &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  
