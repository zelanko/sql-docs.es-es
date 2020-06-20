---
title: Índices de hash | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f4bdc9c1-7922-4fac-8183-d11ec58fec4e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 420cf534b57dc6b6592b4dd55cf5ec2addd04b2a
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84932866"
---
# <a name="hash-indexes"></a>Índices hash
  Los índices se utilizan como puntos de entrada para las tablas optimizadas para memoria. Leer filas de una tabla requiere un índice para buscar los datos en la memoria.  
  
 Un índice hash consta de una colección de cubos organizados en una matriz. Una función hash asigna las claves de índice a los cubos correspondientes en el índice hash. La ilustración siguiente muestra las tres claves de índice que se asignan a tres cubos distintos en el índice hash. Con fines meramente ilustrativos, el nombre de función hash es f(x).  
  
 ![Claves de índice asignadas a diferentes cubos.](../../2014/database-engine/media/hekaton-tables-2.gif "Claves de índice asignadas a diferentes cubos.")  
  
 La función hash que se utiliza para los índices hash tiene las siguientes características:  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tiene una función hash que se utiliza para todos los índices hash.  
  
-   La función hash es determinista. La misma clave de índice se asigna siempre al mismo cubo en el índice hash.  
  
-   Se pueden asignar múltiples claves de índice al mismo depósito de hash.  
  
-   La función hash está equilibrada, lo que significa que la distribución de los valores de clave de índice en los depósitos de hash sigue normalmente una distribución de Poisson.  
  
     La distribución de Poisson no es una distribución uniforme. Los valores de clave de índice no se distribuyen uniformemente en cubos de hash. Por ejemplo, una distribución de Poisson de *n* claves de índice distintas sobre *n* depósitos de hash da como resultado aproximadamente un tercio de cubos vacíos, un tercio de cubos que contienen una clave de índice y el otro tercio que contiene dos claves de índice. Un pequeño número de cubos contendrán más de dos claves.  
  
 Si dos claves de índice se asignan al mismo cubo de hash, hay un conflicto de hash. Un gran número de colisiones de valores hash puede tener un impacto en el rendimiento de las operaciones de lectura.  
  
 La estructura de índice hash en memoria consta de una matriz de punteros de memoria. Cada cubo asigna un desplazamiento en esta matriz. Cada cubo de la matriz señala a la primera fila del cubo de hash. Cada fila del cubo señala a la siguiente fila, por lo que genera una cadena de filas para cada cubo de hash, como se muestra en la ilustración siguiente.  
  
 ![Estructura de índice de hash en memoria.](../../2014/database-engine/media/hekaton-tables-3.gif "Estructura de índice de hash en memoria.")  
  
 La ilustración tiene tres cubos con filas. El segundo cubo de la parte superior contiene las tres filas rojas. El cuarto cubo contiene la única fila azul. El cubo inferior contiene las dos filas verdes. Estas podrían ser versiones diferentes de la misma fila.  
  
 Para obtener más información acerca de los índices para tablas optimizadas para memoria, vea [Guidelines for Using Indexes on Memory-Optimized Tables](../relational-databases/in-memory-oltp/memory-optimized-tables.md):  
  
## <a name="see-also"></a>Consulte también  
 [Índices en tablas optimizadas para memoria](../../2014/database-engine/indexes-on-memory-optimized-tables.md)  
  
  
