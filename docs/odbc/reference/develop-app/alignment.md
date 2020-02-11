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
ms.openlocfilehash: b8b5a107f5ed8cd1c6c45317e60cc515a2601316
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68077271"
---
# <a name="alignment"></a>Alignment
Los problemas de alineación en una aplicación ODBC no suelen ser diferentes de los de cualquier otra aplicación. Es decir, la mayoría de las aplicaciones ODBC tienen pocos o ningún problema con la alineación. Las penalizaciones por no alinear las direcciones varían con el hardware y el sistema operativo, y pueden ser tan pequeñas como una ligera disminución del rendimiento o como un error grave en tiempo de ejecución. Por lo tanto, las aplicaciones ODBC y las aplicaciones ODBC portables en concreto deben tener cuidado al alinear los datos correctamente.  
  
 Un ejemplo de cuándo las aplicaciones ODBC presentan problemas de alineación es cuando asignan un gran bloque de memoria y enlazan diferentes partes de esa memoria a las columnas de un conjunto de resultados. Lo más probable es que se produzca cuando una aplicación genérica debe determinar la forma de un conjunto de resultados en tiempo de ejecución y asignar y enlazar memoria en consecuencia.  
  
 Por ejemplo, supongamos que una aplicación ejecuta una instrucción **Select** escrita por el usuario y captura los resultados de esta instrucción. Dado que la forma de este conjunto de resultados no se conoce cuando se escribe el programa, la aplicación debe determinar el tipo de cada columna una vez creado el conjunto de resultados y enlazar la memoria en consecuencia. La forma más fácil de hacerlo es asignar un gran bloque de memoria y enlazar diferentes direcciones de ese bloque a cada columna. Para tener acceso a los datos de una columna, la aplicación convierte la memoria enlazada a esa columna.  
  
 En el diagrama siguiente se muestra un conjunto de resultados de ejemplo y cómo se puede enlazar un bloque de memoria mediante el tipo de datos C predeterminado para cada tipo de datos de SQL. Cada "X" representa un único byte de memoria. (En este ejemplo se muestran solo los búferes de datos que están enlazados a las columnas. Esto se hace por simplicidad. En el código real, también se deben alinear los búferes de longitud/indicador).  
  
 ![Enlace por tipo de datos C predeterminado a tipo de datos SQL](../../../odbc/reference/develop-app/media/pr24.gif "pr24")  
  
 Suponiendo que las direcciones enlazadas se almacenan en la matriz de *direcciones* , la aplicación usa las siguientes expresiones para tener acceso a la memoria enlazada a cada columna:  
  
```  
(SQLCHAR *)       Address[0]  
(SQLSMALLINT *)   Address[1]  
(SQLINTEGER *)    Address[2]  
```  
  
 Tenga en cuenta que las direcciones enlazadas a la segunda y tercera columnas comienzan en bytes impares y que la dirección enlazada a la tercera columna no es divisible por cuatro, que es el tamaño de un SDWORD. En algunos equipos, esto no será un problema. en otros, se producirá una ligera disminución del rendimiento. en otros, se producirá un error grave en tiempo de ejecución. Una solución mejor sería alinear cada dirección enlazada en su límite de alineación natural. Suponiendo que es 1 para un UCHAR, 2 para un arma y 4 para un SDWORD, esto daría el resultado que se muestra en la siguiente ilustración, donde una "X" representa un byte de memoria que se usa y una "O" representa un byte de memoria que no se utiliza.  
  
 ![Enlace por límite de alineación natural](../../../odbc/reference/develop-app/media/pr25.gif "pr25")  
  
 Aunque esta solución no usa toda la memoria de la aplicación, no detecta ningún problema de alineación. Desafortunadamente, se necesita una cantidad equitativa de código para implementar esta solución, ya que cada columna debe alinearse individualmente según su tipo. Una solución más sencilla consiste en alinear todas las columnas en el tamaño del límite de alineación mayor, que es 4 en el ejemplo que se muestra en la siguiente ilustración.  
  
 ![Enlace por límite de alineación mayor](../../../odbc/reference/develop-app/media/pr26.gif "pr26")  
  
 Aunque esta solución deja huecos mayores, el código para implementarlo es relativamente sencillo y rápido. En la mayoría de los casos, esto compensa la penalización pagada en la memoria sin usar. Para obtener un ejemplo en el que se usa este método, vea [usar SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md).
