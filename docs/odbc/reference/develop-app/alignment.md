---
title: Alineación | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e4c86fd8fba66e6424b41fa4b80b42fc089e6d64
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47853882"
---
# <a name="alignment"></a>Alignment
Los problemas de alineación en una aplicación ODBC generalmente no son diferentes de ellos se encuentran en cualquier otra aplicación. Es decir, la mayoría de las aplicaciones ODBC tienen pocos o ningún problemas con la alineación. Las penalizaciones de direcciones no se alinee varían con el hardware y sistema operativo y podrían ser como secundaria como una ligera disminución del rendimiento o tan grave como un error grave de tiempo de ejecución. Por lo tanto, las aplicaciones ODBC y las aplicaciones ODBC portables en concreto, deben tener cuidado para alinear los datos correctamente.  
  
 Un ejemplo de cuándo las aplicaciones ODBC produce problemas de alineación es cuando se asignan un bloque grande de memoria y enlazar las distintas partes de la memoria a las columnas de un conjunto de resultados. Esto suele ocurrir cuando una aplicación genérica debe determinar la forma de un conjunto de resultados en tiempo de ejecución y asignar y enlazar la memoria en consecuencia.  
  
 Por ejemplo, suponga que una aplicación ejecuta un **seleccione** instrucción escrita por el usuario y recupera los resultados de esta instrucción. Dado que la forma de este conjunto de resultados no se conoce cuando se escribe el programa, la aplicación debe determinar el tipo de cada columna una vez creado el conjunto de resultados y enlazar la memoria en consecuencia. La manera más fácil de hacerlo es asignar un bloque grande de memoria y enlazar diferentes direcciones en ese bloque a cada columna. Para obtener acceso a los datos de una columna, la aplicación convierte la memoria enlazada a esa columna.  
  
 El siguiente diagrama muestra un resultado de ejemplo establece y cómo se puede enlazar un bloque de memoria a ella mediante el tipo de datos C predeterminado para cada tipo de datos SQL. Cada "X" representa un solo byte de memoria. (Este ejemplo muestra solo los búferes de datos que están enlazados a las columnas. Esto se hace por motivos de simplicidad. En el código real, los búferes de longitud/indicador también deben estar alineados.)  
  
 ![Enlace por tipo de datos C predeterminado a tipo de datos SQL](../../../odbc/reference/develop-app/media/pr24.gif "pr24")  
  
 Suponiendo que las direcciones de enlace se almacenan en el *dirección* matriz, la aplicación usa las siguientes expresiones para tener acceso a la memoria que se enlaza a cada columna:  
  
```  
(SQLCHAR *)       Address[0]  
(SQLSMALLINT *)   Address[1]  
(SQLINTEGER *)    Address[2]  
```  
  
 Tenga en cuenta que las direcciones se enlaza a la segunda y tercera columnas iniciar en el número impar de bytes y que la dirección enlazada a la tercera columna no es divisible por cuatro, que es el tamaño de un SDWORD. En algunos equipos, esto no será un problema; en otros, provocará una ligera disminución del rendimiento; en otros, provocará un error irrecuperable de tiempo de ejecución. Una mejor solución sería alinear cada dirección enlazada en su límite de alineación natural. Suponiendo que esto es 1 para un UCHAR, 2 para una ESPADA y 4 para una SDWORD, esto daría el resultado que se muestra en la ilustración siguiente, donde una "X" representa un byte de memoria que se usa y una "O" representa un byte de memoria que se utiliza.  
  
 ![Enlace por límite de alineación natural](../../../odbc/reference/develop-app/media/pr25.gif "pr25")  
  
 Aunque esta solución no utiliza toda memoria de la aplicación, no encuentra algún problema de alineación. Por desgracia, toma una gran cantidad de código para implementar esta solución, como cada columna deben estar alineada individualmente según su tipo. Una solución más sencilla consiste en Alinear todas las columnas en el tamaño del límite de alineación mayor, que es 4 en el ejemplo se muestra en la siguiente ilustración.  
  
 ![Enlace por límite de alineación mayor](../../../odbc/reference/develop-app/media/pr26.gif "pr26")  
  
 Aunque esta solución deja agujeros de mayor tamaño, el código para su implementación es relativamente sencilla y rápida. En la mayoría de los casos, esto compensa la penalización de pago en memoria no utilizada. Para obtener un ejemplo que usa este método, consulte [utilizando SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md).
