---
title: Alineación ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- alignment issues [ODBC]
ms.assetid: 06a01e51-e7a5-495f-aa27-e304b0d005ff
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 205cc3ff95dd60db215150f46ae894fbb99bd9ff
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288610"
---
# <a name="alignment"></a>Alignment
Los problemas de alineación en una aplicación ODBC generalmente no son diferentes de los que están en cualquier otra aplicación. Es decir, la mayoría de las aplicaciones ODBC tienen pocos o ningún problema con la alineación. Las penalizaciones por no alinear direcciones varían con el hardware y el sistema operativo y pueden ser tan menores como una ligera penalización de rendimiento o tan importantes como un error fatal en tiempo de ejecución. Por lo tanto, las aplicaciones ODBC y las aplicaciones ODBC portátiles en particular, deben tener cuidado de alinear los datos correctamente.  
  
 Un ejemplo de cuándo las aplicaciones ODBC encuentran problemas de alineación es cuando asignan un bloque grande de memoria y enlazan diferentes partes de esa memoria a las columnas de un conjunto de resultados. Esto es más probable que ocurra cuando una aplicación genérica debe determinar la forma de un conjunto de resultados en tiempo de ejecución y asignar y enlazar la memoria en consecuencia.  
  
 Por ejemplo, supongamos que una aplicación ejecuta una instrucción **SELECT** introducida por el usuario y recupera los resultados de esta instrucción. Dado que la forma de este conjunto de resultados no se conoce cuando se escribe el programa, la aplicación debe determinar el tipo de cada columna después de crear el conjunto de resultados y enlazar la memoria en consecuencia. La forma más fácil de hacerlo es asignar un gran bloque de memoria y enlazar diferentes direcciones en ese bloque a cada columna. Para tener acceso a los datos de una columna, la aplicación convierte la memoria enlazada a esa columna.  
  
 En el diagrama siguiente se muestra un conjunto de resultados de ejemplo y cómo se puede enlazar un bloque de memoria mediante el tipo de datos C predeterminado para cada tipo de datos SQL. Cada "X" representa un solo byte de memoria. (Este ejemplo muestra solo los búferes de datos que están enlazados a las columnas. Esto se hace para la simplicidad. En el código real, los búferes de longitud/indicador también deben estar alineados.)  
  
 ![Enlace por tipo de datos C predeterminado a tipo de datos SQL](../../../odbc/reference/develop-app/media/pr24.gif "pr24")  
  
 Suponiendo que las direcciones enlazadas se almacenan en la matriz *Address,* la aplicación utiliza las siguientes expresiones para tener acceso a la memoria enlazada a cada columna:  
  
```  
(SQLCHAR *)       Address[0]  
(SQLSMALLINT *)   Address[1]  
(SQLINTEGER *)    Address[2]  
```  
  
 Observe que las direcciones enlazadas a la segunda y tercera columnas comienzan en bytes impares y que la dirección enlazada a la tercera columna no es divisible por cuatro, que es el tamaño de un SDWORD. En algunas máquinas, esto no será un problema; en otros, causará una ligera penalización de rendimiento; en otros, causará un error fatal en tiempo de ejecución. Una mejor solución sería alinear cada dirección enlazada en su límite de alineación natural. Suponiendo que esto es 1 para un UCHAR, 2 para un SWORD y 4 para un SDWORD, esto daría el resultado que se muestra en la siguiente ilustración, donde una "X" representa un byte de memoria que se utiliza y una "O" representa un byte de memoria que no se utiliza.  
  
 ![Enlace por límite de alineación natural](../../../odbc/reference/develop-app/media/pr25.gif "pr25")  
  
 Aunque esta solución no utiliza toda la memoria de la aplicación, no encuentra ningún problema de alineación. Desafortunadamente, se necesita una buena cantidad de código para implementar esta solución, ya que cada columna debe estar alineada individualmente según su tipo. Una solución más sencilla es alinear todas las columnas en el tamaño del límite de alineación más grande, que es 4 en el ejemplo que se muestra en la siguiente ilustración.  
  
 ![Enlace por límite de alineación mayor](../../../odbc/reference/develop-app/media/pr26.gif "pr26")  
  
 Aunque esta solución deja agujeros más grandes, el código para implementarlo es relativamente simple y rápido. En la mayoría de los casos, esto compensa la penalización pagada en la memoria no utilizada. Para obtener un ejemplo que utiliza este método, vea Uso de [SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md).
