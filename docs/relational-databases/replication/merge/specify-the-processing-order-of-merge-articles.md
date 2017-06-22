---
title: "Especificar el orden de procesamiento de los artículos de mezcla | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- articles [SQL Server replication], processing order
- merge replication [SQL Server replication], article processing order
ms.assetid: d151e2c5-cf50-4cb3-a829-8f32455dbd66
caps.latest.revision: 34
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 8682c27e9d94410f8ffc902d2c03af491ec758ba
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="specify-the-processing-order-of-merge-articles"></a>Especificar el orden de procesamiento de los artículos de mezcla
  Desde [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], es posible invalidar el orden predeterminado del procesamiento de artículos para las publicaciones de combinación. Esto resulta útil, por ejemplo, si define la integridad referencial a través de desencadenadores que se deben activar en un orden determinado.  
  
 **Para especificar el orden de procesamiento de los artículos**  
  
-   Programación de Transact-SQL de replicación: [Especificar el orden de procesamiento de la mezcla de artículos de tabla &#40;programación de la replicación con Transact-SQL&#41;](../../../relational-databases/replication/publish/specify-the-processing-order-of-merge-table-articles.md)  
  
## <a name="how-processing-order-is-determined"></a>Cómo se determina el orden de procesamiento  
 De manera predeterminada, durante la sincronización de mezcla, los artículos se procesan en el orden requerido por las dependencias entre objetos, incluidas las restricciones de integridad referencial declarativa (DRI) definidas en las tablas base. El procesamiento implica enumerar los cambios de una tabla y aplicar esos cambios a continuación. Si no hay DRI presente pero hay filtros de combinación o registros lógicos entre los artículos de la tabla, los artículos se procesan en el orden que requieran los filtros y los registros lógicos. Los artículos que no estén relacionados con ningún otro artículo mediante DRI, filtros de combinación, registros lógicos u otras dependencias, se procesan según el alias del artículo de la tabla de sistema [sysmergearticles &#40;Transact-SQL&#41;](../../../relational-databases/system-tables/sysmergearticles-transact-sql.md).  
  
 Imagine una publicación que incluye las tablas **SalesOrderHeader** y **SalesOrderDetail** con una columna de clave principal **SalesOrderID** en la tabla **SalesOrderHeader** y una columna de clave externa correspondiente **SalesOrderID** en la tabla **SalesOrderDetail** . Durante la sincronización, la replicación de mezcla impide infracciones de clave externa insertando cualquier fila nueva en **SalesOrderHeader** antes de insertar filas asociadas en **SalesOrderDetail**. De forma similar, las filas se eliminan de **SalesOrderDetail** antes de que la fila asociada se elimine de **SalesOrderHeader**.  
  
 Sin embargo, en algunas aplicaciones, la integridad referencial se ve reforzada mediante desencadenadores de base de datos, o en el nivel de aplicación, y no mediante DRI. Si tomamos la publicación descrita más arriba, en vez de DRI, la tabla **SalesOrderDetail** podría tener un desencadenador de inserción que asegure que la fila asociada en la tabla **SalesOrderHeader** exista antes de permitir una inserción. **SalesOrderHeader** podría tener un desencadenador de eliminación que asegure que no haya filas asociadas en **SalesOrderDetail** antes de permitir una eliminación. La replicación de mezcla no tiene en cuenta los desencadenadores cuando determina el orden de procesamiento de artículos porque no puede determinar los resultados del desencadenador hasta que se haya activado. De forma similar, la replicación no puede tener en cuenta las restricciones definidas en el nivel de aplicación.  
  
 Cuando la integridad referencial se mantiene a través de los desencadenadores o en el nivel de aplicación, debe especificar el orden en el que se deben procesar los artículos. En el ejemplo con desencadenadores, debería especificar que la tabla **SalesOrderHeader** se debe procesar antes que **SalesOrderDetail**, puesto que el orden de los artículos se basa en el orden de inserción. La replicación de mezcla invertirá automáticamente el orden de las eliminaciones. La replicación de mezcla no producirá ningún error sin el orden de los artículos, porque el Agente de mezcla sigue procesando artículos si se produce una infracción de restricción. Lo que hace es reintentar las operaciones que hayan dado error cuando los otros artículos se hayan terminado de procesar. Especificar el orden de los artículos únicamente impide los reintentos y los procesos adicionales asociados con ellos. Si especifica un orden incorrecto (por ejemplo, uno que dé como resultado el procesamiento de los registros de detalle antes que el de los registros de encabezado), la replicación de mezcla volverá a realizar el proceso hasta que lo consiga.  
  
## <a name="see-also"></a>Vea también  
 [Article Options for Merge Replication](../../../relational-databases/replication/merge/article-options-for-merge-replication.md)  (Opciones de artículos para replicación de mezcla)  
 [Agrupar cambios en filas relacionadas con registros lógicos](../../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)   
 [Join Filters](../../../relational-databases/replication/merge/join-filters.md)  
  
  
