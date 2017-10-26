---
title: "Hacer copia de seguridad de una base de datos con tablas con optimización para memoria | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 83d47694-e56d-4dae-b54e-14945bf8ba31
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 43fa6642db8924195fa1291d74291c21d0b064d1
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="backing-up-a-database-with-memory-optimized-tables"></a>Hacer copia de seguridad de una base de datos con tablas con optimización para memoria
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  La copia de seguridad de las tablas con optimización para memoria se realiza como parte de las copias de seguridad periódicas de las bases de datos. En cuanto a las tablas basadas en disco, la función CHECKSUM de los pares de archivos de datos y delta se valida como parte de la copia de seguridad de la base de datos para detectar si hay daños en el almacenamiento.  
  
> [!NOTE]  
>  Durante una copia de seguridad, si detecta un error de SUMA DE COMPROBACIÓN en uno o varios archivos de un grupo de archivos con optimización para memoria, se producirá un error en la operación de copia de seguridad. En esa situación, debe restaurar la base de datos a partir de la última copia de seguridad buena conocida.  
>   
>  Si no tiene una copia de seguridad, puede exportar los datos de las tablas con optimización para memoria y las tablas basadas en disco y recargarlos después de quitar y volver a crear la base de datos.  
  
 Una copia de seguridad completa de una base de datos con una o más tablas con optimización para memoria consta del almacenamiento asignado para las tablas basadas en disco (si existen), el registro de transacciones activo, y los pares de archivos de datos y delta (también conocidos como pares de archivos de punto de comprobación) para las tablas con optimización para memoria. Pero como se describe en [Durabilidad de las tablas con optimización para memoria](../../relational-databases/in-memory-oltp/durability-for-memory-optimized-tables.md), el almacenamiento que usan las tablas con optimización para memoria puede ser mucho mayor que el tamaño de la memoria y eso afecta al tamaño de la copia de seguridad de la base de datos.  
  
## <a name="full-database-backup"></a>Copia de seguridad completa de base de datos  
 Esta explicación se centra en las copias de seguridad de las bases de datos que solo tienen tablas durables con optimización para memoria, ya que la copia de seguridad para las tablas basadas en disco es igual. Los pares de archivos de punto de comprobación del grupo de archivos con optimización para memoria pueden estar en varios estados. En la tabla siguiente se describe de qué parte de los archivos se hace copia de seguridad.  
  
|Estado del par de archivos de punto de comprobación|Backup|  
|--------------------------------|------------|  
|PRECREATED|Solo metadatos de archivo|  
|UNDER CONSTRUCTION|Solo metadatos de archivo|  
|ACTIVO|Metadatos de archivo y bytes usados|  
|MERGE TARGET|Solo metadatos de archivo|  
|WAITING FOR LOG TRUNCATION|Metadatos de archivo y bytes usados|  
  
 Para obtener descripciones de los estados de los pares de archivos de punto de comprobación, vea [sys.dm_db_xtp_checkpoint_files &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md) y su columna state_desc.  
  
 El tamaño de las copias de seguridad de base de datos con una o varias tablas con optimización para memoria suele ser mayor que su tamaño en memoria pero menor que el almacenamiento en disco. El tamaño adicional depende del número de filas eliminadas, entre otros factores.  
  
### <a name="estimating-size-of-full-database-backup"></a>Estimar el tamaño de una copia de seguridad completa de base de datos  
  
> [!IMPORTANT]  
>  Se recomienda no usar el valor BackupSizeInBytes para estimar el tamaño de la copia de seguridad para OLTP en memoria.  
  
 El primer escenario de carga de trabajo es (principalmente) para operaciones de inserción. En este escenario, la mayoría de los archivos de datos tienen el estado Active, totalmente cargados y con muy pocas filas eliminadas. El tamaño de la copia de seguridad de base de datos es similar al tamaño de los datos en memoria.  
  
 El segundo escenario de carga de trabajo es para las operaciones frecuentes de inserción, eliminación y actualización. En el peor de los casos, cada uno de los pares de archivos de punto de comprobación se carga al 50 %, después de tener en cuenta las filas eliminadas. El tamaño de la copia de seguridad de base de datos será al menos el doble que el tamaño de los datos en memoria.  
  
## <a name="differential-backups-of-databases-with-memory-optimized-tables"></a>Copias de seguridad diferenciales de bases de datos con tablas con optimización para memoria  
 El almacenamiento de las tablas con optimización para memoria consta de archivos delta y de datos como se describe en [Durabilidad de las tablas con optimización para memoria](../../relational-databases/in-memory-oltp/durability-for-memory-optimized-tables.md). La copia de seguridad diferencial de una base de datos con tablas con optimización para memoria contiene los datos siguientes:  
  
-   La copia de seguridad diferencial de los grupos de archivos que almacenan las tablas basadas en disco no se ve afectada por la presencia de tablas con optimización para memoria.  
  
-   El registro de transacciones activo es igual que en una copia de seguridad completa de la base de datos.  
  
-   Para un grupo de archivos de datos con optimización para memoria, la copia de seguridad diferencial utiliza el mismo algoritmo que la copia de seguridad completa de la base de datos para identificar los archivos delta y de datos de la copia de seguridad pero después filtra el subconjunto de archivos como sigue:  
  
    -   Un archivo de datos contiene filas recién insertadas y, cuando está lleno, se cierra y se marca como de solo lectura. Se hace una copia de seguridad de un archivo de datos solo si se ha cerrado después de la última copia de seguridad completa de la base de datos. La copia de seguridad diferencial solo copia los archivos de datos que contienen las filas insertadas desde la última copia de seguridad completa de la base de datos. Una excepción es un escenario de actualización y eliminación donde es posible que algunas de las filas insertadas puedan haberse marcado ya para recolección de elementos no utilizados o que sus elementos no utilizados ya se hayan recolectado.  
  
    -   Los archivos delta almacenan las referencias a las filas de datos eliminadas. Puesto que las transacciones futuras pueden eliminar una fila, un archivo delta se puede modificar en cualquier momento durante su tiempo de vida, nunca se cierra. Siempre se hace una copia de seguridad de un archivo delta. Los archivos delta suelen utilizar menos del 10 % del almacenamiento, de modo que los archivos delta tienen un efecto mínimo en el tamaño de la copia de seguridad diferencial.  
  
 Si las tablas con optimización para memoria son una parte significativa del tamaño de la base de datos, la copia de seguridad diferencial puede reducir considerablemente el tamaño de la copia de seguridad de la base de datos. Para las cargas de trabajo OLTP habituales, las copias de seguridad diferenciales serán mucho menores que las copias de seguridad completas de base de datos.  
  
## <a name="see-also"></a>Vea también  
 [Hacer copia de seguridad, restaurar y recuperar tablas con optimización para memoria](http://msdn.microsoft.com/library/3f083347-0fbb-4b19-a6fb-1818d545e281)  
  
  

