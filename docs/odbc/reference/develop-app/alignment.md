---
title: "Alineación | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- alignment issues [ODBC]
ms.assetid: 06a01e51-e7a5-495f-aa27-e304b0d005ff
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 412c04f8181997738bac1fc7b457c9ec0c3efcde
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="alignment"></a>Alignment
Los problemas de alineación en una aplicación ODBC generalmente no son diferentes de están en cualquier otra aplicación. Es decir, la mayoría de las aplicaciones de ODBC tiene problemas de pocos o ningún con alineación. Las penalizaciones por no alinear direcciones varían según el hardware y el sistema operativo y podrían ser como secundaria como una ligera disminución del rendimiento o tan grave como un error irrecuperable de tiempo de ejecución. Por lo tanto, las aplicaciones ODBC y las aplicaciones ODBC portables en concreto, deberían tener precaución alinear los datos correctamente.  
  
 Un ejemplo de cuando las aplicaciones ODBC encuentran problemas de alineación es cuando se asignan un bloque grande de memoria y enlazar diferentes partes de la memoria a las columnas de un conjunto de resultados. Esto es más probable que se producen cuando una aplicación genérica debe determinar la forma de un conjunto de resultados en tiempo de ejecución y asignar y enlace memoria en consecuencia.  
  
 Por ejemplo, suponga que una aplicación ejecuta un **seleccione** instrucción especificados por el usuario y recupera los resultados de esta instrucción. Dado que la forma de este conjunto de resultados no se conoce cuando se escribe el programa, la aplicación debe determinar el tipo de cada columna una vez creado el conjunto de resultados y enlazar memoria en consecuencia. La manera más fácil de hacerlo es asignar un bloque grande de memoria y enlazar direcciones diferentes dentro de dicho bloque a cada columna. Para obtener acceso a los datos de una columna, la aplicación convierte la memoria enlazada a esa columna.  
  
 El siguiente diagrama muestra un resultado de ejemplo establece y cómo se puede enlazar un bloque de memoria a él utilizando el tipo de datos C predeterminado para cada tipo de datos SQL. Cada "X" representa un solo byte de memoria. (Este ejemplo muestra solo los búferes de datos que están enlazados a las columnas. Esto sirve para simplificar el trabajo. En el código real, los búferes de longitud/indicador también se deben alinear.)  
  
 ![Enlace por tipo de datos C predeterminado a tipo de datos SQL](../../../odbc/reference/develop-app/media/pr24.gif "pr24")  
  
 Suponiendo que las direcciones de enlace se almacenan en la *dirección* matriz, la aplicación utiliza las siguientes expresiones para tener acceso a la memoria que se enlaza a cada columna:  
  
```  
(SQLCHAR *)       Address[0]  
(SQLSMALLINT *)   Address[1]  
(SQLINTEGER *)    Address[2]  
```  
  
 Observe que las direcciones se enlaza a la segunda y tercera columnas iniciar en número impar de bytes y que la dirección enlazada a la tercera columna no es divisible por cuatro, que es el tamaño de una SDWORD. En algunos equipos, esto no será un problema; en otras versiones, provocará una ligera disminución del rendimiento; en otras todavía, provocará un error irrecuperable de tiempo de ejecución. Una mejor solución sería alinear cada dirección enlazado en su límite de alineación natural. Suponiendo que se trata de 1 para un UCHAR, 2 para un filo y 4 para un SDWORD, esto daría el resultado que se muestra en la ilustración siguiente, donde una "X" representa un byte de memoria que se utiliza y una "O" representa un byte de memoria que se utiliza.  
  
 ![Enlace por límite de alineación natural](../../../odbc/reference/develop-app/media/pr25.gif "pr25")  
  
 Aunque esta solución no utiliza toda la memoria de la aplicación, no encuentra algún problema de alineación. Por desgracia, toma una cantidad considerable de código para implementar esta solución, como cada columna debe estar alineada individualmente según su tipo. Es una solución más sencilla alinear todas las columnas en el tamaño de los límites de alineación más grande, que es 4 en el ejemplo se muestra en la siguiente ilustración.  
  
 ![Enlace por límite de alineación mayor](../../../odbc/reference/develop-app/media/pr26.gif "pr26")  
  
 Aunque esta solución deja agujeros mayor, el código para implementarlo es relativamente sencillo y rápido. En la mayoría de los casos, Esto desplaza la penalización de pago en memoria no utilizada. Para obtener un ejemplo que utiliza este método, consulte [utilizando SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md).
