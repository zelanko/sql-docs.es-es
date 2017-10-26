---
title: "Creación y administración del almacenamiento de objetos con optimización para memoria | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 622aabe6-95c7-42cc-8768-ac2e679c5089
caps.latest.revision: 64
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2b955ffcf895f5356b77e0d772b3f1ac0cd9780e
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="creating-and-managing-storage-for-memory-optimized-objects"></a>Crear y administrar el almacenamiento de objetos con optimización para memoria
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  El motor de [!INCLUDE[hek_2](../../includes/hek-2-md.md)] está integrado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], que le permite tener las tablas con optimización para memoria y las tablas basadas en disco (tradicionales) en la misma base de datos. Sin embargo, la estructura de almacenamiento para tablas con optimización para memoria es diferente de las tablas basadas en disco.  
  
 El almacenamiento para tablas basadas en disco tiene los siguientes atributos clave:  
  
-   Está asignado a un grupo de archivos y el grupo de archivos contiene uno o más archivos.  
  
-   Cada archivo está dividido en extensiones de 8 páginas y cada página tiene 8 KB.  
  
-   Una extensión se puede compartir entre varias tablas, pero hay una asignación 1 a 1 entre una página asignada y la tabla o índice. En otras palabras, una página no puede tener filas de dos o más tablas o índices.  
  
-   Los datos se mueven a la memoria (el grupo de búferes) según sea necesario y las páginas modificadas o recién creadas se escriben asincrónicamente en el disco que genera la E/S principalmente aleatoria.  
  
 El almacenamiento de tablas con optimización para memoria tiene los siguientes atributos clave:  
  
-   Todas las tablas con optimización para memoria se asignan a un grupo de archivos de datos con optimización para memoria. Este grupo de archivos utiliza una sintaxis y semántica similar a Filestream.  
  
-   No existen páginas y los datos se guardan como una fila.  
  
-   Todos los cambios realizados en las tablas con optimización para memoria se almacenan anexándolos a los archivos activos. Tanto la lectura como la escritura en los archivos son secuenciales.  
  
-   Una actualización se implementa como una eliminación seguida de una inserción. Las filas eliminadas no se quitan inmediatamente del almacenamiento. Las filas eliminadas se quitan mediante un proceso en segundo plano, denominado MERGE, según una directiva como se describe en [Durabilidad de las tablas con optimización para memoria](../../relational-databases/in-memory-oltp/durability-for-memory-optimized-tables.md).  
  
-   A diferencia de las tablas basadas en disco, el almacenamiento de tablas con optimización para memoria no se comprime. Al migrar una tabla basada en disco (ROW o PAGE) comprimida tabla a una tabla con optimización para memoria, debe tener en cuenta el cambio del tamaño.  
  
-   Una tabla con optimización para memoria puede ser durable o no durable. Solo tiene que configurar el almacenamiento para las tablas con optimización para memoria durables.  
  
 En esta sección se describen los pares de archivos de punto de comprobación y otros aspectos de cómo se almacenan los datos en tablas con optimización para memoria.  
  
 Temas de esta sección:  
  
-   [Configurar el almacenamiento para las tablas con optimización para memoria](../../relational-databases/in-memory-oltp/configuring-storage-for-memory-optimized-tables.md)  
  
-   [El grupo de archivos con optimización para memoria](../../relational-databases/in-memory-oltp/the-memory-optimized-filegroup.md)  
  
-   [Durabilidad de las tablas con optimización para memoria](../../relational-databases/in-memory-oltp/durability-for-memory-optimized-tables.md)  
  
-   [Funcionamiento de los puntos de comprobación para tablas con optimización para memoria](../../relational-databases/in-memory-oltp/checkpoint-operation-for-memory-optimized-tables.md)  
  
-   [Definir la durabilidad de los objetos con optimización para memoria](../../relational-databases/in-memory-oltp/defining-durability-for-memory-optimized-objects.md)  
  
-   [Comparar el almacenamiento de tablas basadas en disco con el almacenamiento de tablas con optimización para memoria](../../relational-databases/in-memory-oltp/comparing-disk-based-table-storage-to-memory-optimized-table-storage.md)  
  
## <a name="see-also"></a>Vea también  
 [OLTP en memoria &#40;optimización en memoria&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  

