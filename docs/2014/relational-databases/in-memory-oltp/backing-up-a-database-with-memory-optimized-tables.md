---
title: Hacer copia de seguridad de una base de datos con tablas con optimización para memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 83d47694-e56d-4dae-b54e-14945bf8ba31
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: bc4da6702716e845121d2081a166254d4be9449f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62468331"
---
# <a name="backing-up-a-database-with-memory-optimized-tables"></a>Hacer copia de seguridad de una base de datos con tablas con optimización para memoria
  La copia de seguridad de las tablas con optimización para memoria se realiza como parte de las copias de seguridad periódicas de las bases de datos. En cuanto a las tablas basadas en disco, la función CHECKSUM de los pares de archivos de datos y delta se valida como parte de la copia de seguridad de la base de datos para detectar si hay daños en el almacenamiento.  
  
> [!NOTE]  
>  Durante una copia de seguridad, si detecta un error de suma de comprobación en uno o más archivos de un grupo de archivos optimizados para memoria, no podrá restaurar y reiniciar la base de datos. En esa situación, debe restaurar la base de datos con la última copia de seguridad buena conocida. Si no tiene una copia de seguridad, puede exportar los datos de las tablas optimizadas para memoria y las tablas basadas en disco, y recargarlos después de quitar y volver a crear la base de datos.  
  
 Una copia de seguridad completa de una base de datos con una o más tablas optimizadas para memoria consta del almacenamiento asignado para las tablas basadas en disco (si existen), el registro de transacciones activo, y los pares de archivos de datos y delta (también conocidos como pares de archivos de punto de comprobación) para las tablas optimizadas para memoria. Pero como se describe en [Durabilidad de las tablas optimizadas para memoria](memory-optimized-tables.md), el almacenamiento que usan las tablas optimizadas para memoria puede ser mucho mayor que el tamaño de la memoria y eso afecta al tamaño de la copia de seguridad de la base de datos.  
  
## <a name="full-database-backup"></a>Copia de seguridad completa de base de datos  
 Esta explicación se centrará en las copias de seguridad de las bases de datos que solo tienen tablas durables optimizadas para memoria, ya que la copia de seguridad para las tablas basadas en disco es igual. Los pares de archivos de punto de comprobación del grupo de archivos optimizados para memoria pueden estar en varios estados. En la tabla siguiente se describe de qué parte de los archivos se hace copia de seguridad.  
  
|Estado del par de archivos de punto de comprobación|Copia de seguridad|  
|--------------------------------|------------|  
|PRECREATED|Solo metadatos de archivo|  
|UNDER CONSTRUCTION|Solo metadatos de archivo|  
|Activo|Metadatos de archivo y bytes usados|  
|Merge source|Metadatos de archivo y bytes usados|  
|Merge target|Solo metadatos de archivo|  
|REQUIRED FOR BACKUP/HA|Metadatos de archivo y bytes usados|  
|IN TRANSITION TO TOMBSTONE|Solo metadatos de archivo|  
|TOMBSTONE|Solo metadatos de archivo|  
  
 El tamaño de las copias de seguridad de base de datos con una o más tablas optimizadas para memoria suele ser mayor que su tamaño en memoria pero menor que el almacenamiento en disco. El tamaño adicional dependerá del número de filas eliminadas y el número de pares de archivos de punto de comprobación que estén en los estados Merge source y REQUIRED FOR BACKUP/HA, lo que depende indirectamente de la carga de trabajo. Para obtener descripciones de los Estados de pares de archivos de punto de comprobación, vea [sys.dm_db_xtp_checkpoint_files &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql).  
  
### <a name="estimating-size-of-full-database-backup"></a>Estimar el tamaño de una copia de seguridad completa de base de datos  
  
> [!IMPORTANT]  
>  Se recomienda no usar el valor BackupSizeInBytes para estimar el tamaño de la copia de seguridad para OLTP en memoria.  
  
 El primer escenario de carga de trabajo es (principalmente) para operaciones de inserción. En este escenario, la mayoría de los archivos de datos estarán en el estado Active, totalmente cargados y con muy pocas filas eliminadas. El tamaño de la copia de seguridad de base de datos será similar al tamaño de los datos en memoria.  
  
 El segundo escenario de carga de trabajo es para las operaciones de actualización, eliminación y frecuentes de inserción: En el peor de los casos, cada uno de los pares de archivos de punto de comprobación se carga al 50 %, después de tener en cuenta las filas eliminadas. Por tanto, el tamaño de la copia de seguridad de base de datos será al menos el doble que el tamaño de los datos en memoria. Además, habrá pocos pares de archivos de punto de comprobación en los estados Merge source y Required for backup/high availability que aumenten el tamaño de la copia de seguridad de base de datos.  
  
## <a name="differential-backups-of-databases-with-memory-optimized-tables"></a>Copias de seguridad diferenciales de bases de datos con tablas con optimización para memoria  
 El almacenamiento de las tablas optimizadas para memoria consta de archivos delta y de datos como se describe en [Durabilidad de las tablas optimizadas para memoria](memory-optimized-tables.md). La copia de seguridad diferencial de una base de datos con tablas optimizadas para memoria contiene los datos siguientes:  
  
-   La copia de seguridad diferencial de los grupos de archivos que almacenan las tablas basadas en disco no se ve afectada por la presencia de tablas optimizadas para memoria.  
  
-   El registro de transacciones activo es igual que en una copia de seguridad completa de la base de datos.  
  
-   Para un grupo de archivos de datos optimizados para memoria, la copia de seguridad diferencial utiliza el mismo algoritmo que la copia de seguridad completa de la base de datos para identificar los archivos delta y de datos de la copia de seguridad pero después filtra el subconjunto de archivos como sigue:  
  
    -   Un archivo de datos contiene filas recién insertadas y cuando está lleno, se cierra y se marca como de solo lectura. Se hace una copia de seguridad de un archivo de datos solo si se ha cerrado después de la última copia de seguridad completa de la base de datos. Las copias de seguridad diferenciales solo hacen copia de seguridad de los archivos de datos que contienen las filas insertadas desde la última copia de seguridad completa de la base de datos con la excepción de un escenario de actualización y eliminación donde es posible que algunas filas insertadas se hayan marcado ya para recolección de elementos no utilizados o se hayan eliminado ya mediante el recolector de elementos no utilizados.  
  
    -   Los archivos delta almacenan las referencias a las filas de datos eliminadas. Puesto que las transacciones futuras pueden eliminar una fila, un archivo delta se puede modificar en cualquier momento durante su tiempo de vida, nunca se cierra. Siempre se hace una copia de seguridad de un archivo delta. Los archivos delta suelen utilizar menos del 10 % del almacenamiento, de modo que los archivos delta tienen un efecto mínimo en el tamaño de la copia de seguridad diferencial.  
  
 Si las tablas optimizadas para memoria son una parte significativa del tamaño de la base de datos, la copia de seguridad diferencial puede reducir considerablemente el tamaño de la copia de seguridad de la base de datos.  
  
 Para las cargas de trabajo OLTP habituales, las copias de seguridad diferenciales serán mucho menores que las copias de seguridad completas de base de datos.  
  
## <a name="see-also"></a>Vea también  
 [Hacer copia de seguridad, restaurar y recuperar tablas con optimización para memoria](restore-and-recovery-of-memory-optimized-tables.md)  
  
  
