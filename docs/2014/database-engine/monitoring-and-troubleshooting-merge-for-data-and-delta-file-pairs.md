---
title: Supervisión y solución de problemas de combinación de pares de archivos Delta y de datos | Microsoft Docs
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
ms.openlocfilehash: c7a13345da45d7e6c31a53bc51371306da444a96
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/19/2019
ms.locfileid: "75228179"
---
# <a name="monitoring-and-troubleshooting-merge-for-data-and-delta-file-pairs"></a>Supervisar y solucionar los problemas de la mezcla para los pares de archivos delta y de datos
  OLTP en memoria usa una directiva de mezcla para mezclar los pares de archivos delta y de datos automáticamente. No puede deshabilitar la actividad de mezcla.  
  
 Puede supervisar los pares de archivos delta y de datos como sigue:  
  
-   Compare el tamaño del almacenamiento en memoria con el tamaño total del almacenamiento. Si el almacenamiento es desproporcionadamente grande, es probable que la mezcla no se esté realizando. Para obtener información  
  
-   Observe el espacio usado en los archivos Delta y de datos mediante [Sys. dm_db_xtp_checkpoint_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql) para ver si la combinación no se desencadena cuando debería.  
  
## <a name="performing-a-manual-merge"></a>Realizar una mezcla manual  
 Puede usar [Sys. sp_xtp_merge_checkpoint_files &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-merge-checkpoint-files-transact-sql) para realizar una combinación manual.  
  
 Utilice la siguiente consulta para recuperar información sobre los archivos delta y de datos,  
  
```sql  
select checkpoint_file_id, file_type_desc, internal_storage_slot, file_size_in_bytes, file_size_used_in_bytes,   
inserted_row_count, deleted_row_count, lower_bound_tsn, upper_bound_tsn   
from sys.dm_db_xtp_checkpoint_files  
where state = 1  
order by file_type_desc, upper_bound_tsn  
```  
  
 Supongamos que encontró tres archivos de datos que no se han combinado. Con el valor `lower_bound_tsn` del primer archivo de datos y `upper_bound_tsn` del último, puede emitir el comando siguiente:  
  
```sql  
exec sys.sp_xtp_merge_checkpoint_files 'H_DB',  12345, 67890  
```  
  
 Imagine que los tres pares de archivos delta y de datos tenían cada uno 15.836 filas y 5.279 filas eliminadas. Después de la mezcla, el nuevo archivo de datos tiene 31.872 filas y 0 filas eliminadas. El tamaño del nuevo archivo de datos puede ser mucho mayor que el tamaño asignado inicialmente de 128 MB. Esto se debe a que la mezcla manual invalida la directiva de mezcla y aplica la mezcla de los archivos solicitados.  
  
 La [transición del estado del blog de los archivos de punto de comprobación de las bases de datos con tablas optimizadas para memoria describe la](https://blogs.technet.com/b/dataplatforminsider/archive/2014/01/23/state-transition-of-checkpoint-files-in-databases-with-memory-optimized-tables.aspx) transición de estado de los pares de archivos Delta y de datos desde el inicio hasta la recolección de elementos no utilizados.  
  
## <a name="see-also"></a>Véase también  
 [Crear y administrar el almacenamiento de objetos con optimización para memoria](../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
