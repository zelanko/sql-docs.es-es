---
title: Montones (tablas sin índices agrupados) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- heaps
ms.assetid: df5c4dfb-d372-4d0f-859a-a2d2533ee0d7
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 2a39bac2e0352f2adc7749e980d5cc91044f8ab2
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85025329"
---
# <a name="heaps-tables-without-clustered-indexes"></a>Montones (tablas sin índices agrupados)
  Un montón es una tabla que no tiene un índice clúster. En las tablas almacenadas, se pueden crear uno o varios índices no clúster como un montón. Los datos se almacenan en el montón sin especificar un orden. Normalmente, en un principio los datos se almacenan en el orden en el que las filas se insertan en la tabla, pero [!INCLUDE[ssDE](../../includes/ssde-md.md)] puede mover los datos en el montón para almacenar las filas de forma eficaz, de modo que no se puede predecir el orden de los datos. Para garantizar el orden de las filas que se devuelven de un montón, debe usar la cláusula `ORDER BY`. Para especificar el orden de almacenamiento de las filas, cree un índice clúster en la tabla, de modo que la tabla no sea un montón.  
  
> [!NOTE]  
>  A veces, hay buenos motivos para dejar una tabla como montón en lugar de crear un índice clúster, pero para usar los montones de forma eficaz se requieren conocimientos avanzados. La mayoría de las tablas deben tener un índice clúster cuidadosamente elegido a menos que exista un buen motivo para dejar la tabla como un montón.  
  
## <a name="when-to-use-a-heap"></a>Cuándo se usa un montón  
 Si una tabla es un montón y no tiene ningún índice no clúster, debe examinarse la tabla completa (recorrido de tabla) cuando se busca una fila. Esto puede resultar aceptable si la tabla es pequeña, como una lista con las 12 oficinas regionales de una empresa.  
  
 Cuando una tabla se almacena como un montón, las filas individuales se identifican mediante una referencia a un identificador de fila (RID) que se compone del número de archivo, el número de páginas de datos y el espacio de la página. El identificador de fila es una estructura pequeña y eficaz. A veces, los arquitectos de datos usan montones cuando el acceso a los datos se realiza siempre a través de índices no clúster y el RID es menor que la clave de índice clúster.  
  
## <a name="when-not-to-use-a-heap"></a>Cuándo no se usa un montón  
 No use un montón cuando los datos se devuelvan con frecuencia ordenados. Un índice clúster en la columna de ordenación podría impedir la operación de ordenación.  
  
 No use un montón cuando los datos se agrupan juntos a menudo. Los datos deben estar ordenados antes de que se agrupen y un índice clúster en la columna de ordenación podría impedir la operación de ordenación.  
  
 No use un montón cuando a menudo se consulten rangos de datos de la tabla.  Un índice clúster en la columna de rango impedirá que se ordene el montón completo.  
  
 No use un montón cuando no haya índices no clúster y la tabla sea grande. En un montón, deben leerse todas las filas del montón para buscar una fila.  
  
## <a name="managing-heaps"></a>Administrar montones  
 Para crear un montón, cree una tabla sin un índice clúster. Si la tabla ya tiene un índice clúster, quite el índice clúster para convertir de nuevo la tabla en un montón.  
  
 Para quitar un montón, cree un índice clúster en el montón.  
  
 Para volver a crear un montón a fin de recuperar el espacio desaprovechado, cree un índice clúster en el montón y quítelo después.  
  
> [!WARNING]  
>  Para crear o quitar índices clúster, es necesario volver a escribir toda la tabla. Si la tabla tiene índices no clúster, todos los índices no clúster deberán volver a crearse cada vez que cambie el índice clúster. Por tanto, al convertir un montón en una estructura de índice agrupado o viceversa, puede necesitarse mucho tiempo y gran cantidad de espacio para reordenar los datos en tempdb.  
  
## <a name="related-content"></a>Contenido relacionado  
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)  
  
 [DROP INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-index-transact-sql)  
  
 [Índices agrupados y no agrupados descritos](clustered-and-nonclustered-indexes-described.md)  
  
  
