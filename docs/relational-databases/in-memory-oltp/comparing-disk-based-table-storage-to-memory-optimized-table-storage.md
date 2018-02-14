---
title: "Comparar el almacenamiento de tablas basadas en disco con el almacenamiento de tablas con optimización para memoria | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: in-memory-oltp
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: eacf443c-001a-445f-ad1c-5f5a45eca6f4
caps.latest.revision: 
author: JennieHubbard
ms.author: jhubbard
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e884fda2f5d354856501c11dea5d7631d82e583f
ms.sourcegitcommit: 37f0b59e648251be673389fa486b0a984ce22c81
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/12/2018
---
# <a name="comparing-disk-based-table-storage-to-memory-optimized-table-storage"></a>Comparar el almacenamiento de tablas basadas en disco con el almacenamiento de tablas con optimización para memoria
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  
  
|Categorías|Tabla basada en disco|Tabla perdurable con optimización para memoria|  
|----------------|-----------------------|-------------------------------------|  
|DDL|La información de metadatos se almacena en las tablas del sistema en el grupo de archivos principal de la base de datos y es accesible a través de las vistas de catálogo.|La información de metadatos se almacena en las tablas del sistema en el grupo de archivos principal de la base de datos y es accesible a través de las vistas de catálogo.|  
|Estructura|Las filas se almacenan en páginas de 8 kB. Una página solo almacena filas de la misma tabla.|Las filas se almacenan como filas individuales. No hay ninguna estructura de página. Dos filas consecutivas de un archivo de datos pueden pertenecer a diferentes tablas optimizadas para memoria.|  
|Índices|Los índices se almacenan en una estructura de página similar a las filas de datos.|Solo se conserva la definición del índice (no las filas de índice). Los índices se mantienen en memoria y se regeneran si la tabla optimizada para memoria se carga en la memoria como parte del reinicio de una base de datos. Puesto que no se conservan las filas de índice, no se realiza ningún registro para los cambios de índice.|  
|Operación DML|El primer paso es encontrar la página y cargarla en el grupo de búferes.<br /><br /> Insert<br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inserta la fila en la página teniendo en cuenta la ordenación de las filas en el caso de un índice clúster.<br /><br /> DELETE<br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] busca la fila que se va a eliminar en la página y la marca como eliminada.<br /><br /> Update<br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] busca la fila en la página. La actualización se efectúa en contexto para las columnas que no son de clave. La actualización de la columna de clave se realiza con una operación de inserción y eliminación.<br /><br /> Cuando la operación DML se completa, las páginas afectadas se vacían en el disco como parte de la directiva del grupo de búferes, el punto de comprobación o la confirmación de la transacción para las operaciones registradas mínimamente. Ambas operaciones de lectura/escritura en las páginas conducen a operaciones de E/S innecesarias.|Para las tablas optimizadas para memoria, puesto que los datos residen en memoria, las operaciones DML se realizan directamente en la memoria. Hay un subproceso en segundo plano que lee las entradas del registro para las tablas optimizadas para memoria y las conserva en los archivos de datos y delta. Una actualización genera una nueva versión de fila. Pero se registra una actualización como una eliminación seguida de una inserción.|  
|Fragmentación de datos|La manipulación de datos fragmenta los datos, lo que hace que haya páginas rellenas parcialmente y páginas consecutivas de forma lógica que no son contiguas en el disco. Esto degrada el rendimiento del acceso a los datos y requiere que desfragmente los datos.|Los datos con optimización para memoria no se almacenan en las páginas de modo que no hay fragmentación de los datos. Sin embargo, puesto que se actualizan y eliminan filas, es necesario compactar los archivos delta y de datos. Esto lo hace un subproceso MERGE en segundo plano según una directiva de mezcla.|  
  
## <a name="see-also"></a>Ver también  
 [Crear y administrar el almacenamiento de objetos con optimización para memoria](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
