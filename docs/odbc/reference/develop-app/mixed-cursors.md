---
title: Mixto cursores | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- mixed cursors [ODBC]
- cursors [ODBC], dynamic
- keyset-driven cursors [ODBC]
- dynamic cursors [ODBC]
- cursors [ODBC], key-set driven
- cursors [ODBC], mixed
ms.assetid: 9beb2db9-0b6d-491d-9529-d64e64e59014
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 16fd4840718c286adfe711b6b7322154f7f5f9cb
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="mixed-cursors"></a>Cursores mixtos
Un cursor mixto es una combinación de un cursor controlado por conjunto de claves y un cursor dinámico. Se utiliza cuando el conjunto de resultados es demasiado grande para guardar razonablemente claves para el conjunto de resultados completo. Cursores mixtos se implementan mediante la creación de un conjunto de claves que es menor que el conjunto de resultados completo pero mayor que el conjunto de filas.  
  
 Siempre y cuando la aplicación se desplaza en el conjunto de claves, el comportamiento es controlado por conjunto de claves. Cuando la aplicación se desplaza fuera del conjunto de claves, el comportamiento es dinámico: el cursor recupera las filas solicitadas y crea un nuevo conjunto de claves. Después de crea el conjunto de claves nuevo, el comportamiento revierte al cursor dinámico dentro de ese conjunto de claves.  
  
 Por ejemplo, suponga que un conjunto de resultados tiene 1.000 filas y utiliza un cursor mixto con un tamaño de conjunto de claves de 100 y un tamaño de conjunto de filas de 10. Cuando se captura el primer conjunto de filas, el cursor crea un conjunto de claves que se compone de las claves de las 100 primeras filas. A continuación, devuelve las 10 primeras filas, como se solicitó.  
  
 Ahora suponga que otra aplicación elimina las filas 11 y 101. Si el cursor se intenta recuperar la fila 11, producirá un "agujero" porque tiene una clave para esta fila, pero no hay ninguna fila; se trata de comportamiento de cursor dinámico. Si el cursor se intenta recuperar la fila 101, el cursor no detectará que la fila es que faltan porque no tiene una clave para la fila. En su lugar, se recuperarán que anteriormente era fila 102. Éste es el comportamiento de cursor dinámico.  
  
 Un cursor mixto es equivalente a un cursor controlado por conjunto de claves cuando el tamaño del conjunto de claves es igual que el tamaño del conjunto de resultados. Un cursor mixto es equivalente a un cursor dinámico cuando el tamaño del conjunto de claves es igual a 1.
