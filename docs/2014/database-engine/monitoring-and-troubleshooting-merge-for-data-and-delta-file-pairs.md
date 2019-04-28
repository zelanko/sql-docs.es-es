---
title: Pares de archivos de supervisión y solución de problemas de replicación de mezcla en datos y Delta | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: a8b0bacc-4d2c-42e4-84bf-1a97e0bd385b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 61a9b1697b705e56c73a0b610ae426deb288901e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62844093"
---
# <a name="monitoring-and-troubleshooting-merge-for-data-and-delta-file-pairs"></a>Supervisar y solucionar los problemas de la mezcla para los pares de archivos delta y de datos
  OLTP en memoria usa una directiva de mezcla para mezclar los pares de archivos delta y de datos automáticamente. No puede deshabilitar la actividad de mezcla.  
  
 Puede supervisar los pares de archivos delta y de datos como sigue:  
  
-   Compare el tamaño del almacenamiento en memoria con el tamaño total del almacenamiento. Si el almacenamiento es desproporcionadamente grande, es probable que la mezcla no se esté realizando. Para obtener información  
  
-   Examine el espacio usado en los archivos delta y de datos utilizando [sys.dm_db_xtp_checkpoint_files &#40;Transact-SQL&#41; ](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql) para ver si mezcla no se desencadena cuando debería.  
  
## <a name="performing-a-manual-merge"></a>Realizar una mezcla manual  
 Puede usar [sys.sp_xtp_merge_checkpoint_files &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-merge-checkpoint-files-transact-sql) para realizar una combinación manual.  
  
 Utilice la siguiente consulta para recuperar información sobre los archivos delta y de datos,  
  
```sql  
select checkpoint_file_id, file_type_desc, internal_storage_slot, file_size_in_bytes, file_size_used_in_bytes,   
inserted_row_count, deleted_row_count, lower_bound_tsn, upper_bound_tsn   
from sys.dm_db_xtp_checkpoint_files  
where state = 1  
order by file_type_desc, upper_bound_tsn  
```  
  
 Suponga que encontró tres archivos de datos que no se han combinado. Con el valor `lower_bound_tsn` del primer archivo de datos y `upper_bound_tsn` del último, puede emitir el comando siguiente:  
  
```sql  
exec sys.sp_xtp_merge_checkpoint_files 'H_DB',  12345, 67890  
```  
  
 Imagine que los tres pares de archivos delta y de datos tenían cada uno 15.836 filas y 5.279 filas eliminadas. Después de la mezcla, el nuevo archivo de datos tiene 31.872 filas y 0 filas eliminadas. El tamaño del nuevo archivo de datos puede ser mucho mayor que el tamaño asignado inicialmente de 128 MB. Esto se debe a que la mezcla manual invalida la directiva de mezcla y aplica la mezcla de los archivos solicitados.  
  
 El blog de [transición de estado de archivos punto de comprobación en bases de datos con tablas optimizadas para memoria](http://blogs.technet.com/b/dataplatforminsider/archive/2014/01/23/state-transition-of-checkpoint-files-in-databases-with-memory-optimized-tables.aspx) describe la transición de estado de los datos y delta pares de archivos desde el comienzo a la recolección.  
  
## <a name="see-also"></a>Vea también  
 [Crear y administrar el almacenamiento de objetos con optimización para memoria](../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
