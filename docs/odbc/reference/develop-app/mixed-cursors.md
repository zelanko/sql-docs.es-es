---
title: Mixto cursores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mixed cursors [ODBC]
- cursors [ODBC], dynamic
- keyset-driven cursors [ODBC]
- dynamic cursors [ODBC]
- cursors [ODBC], key-set driven
- cursors [ODBC], mixed
ms.assetid: 9beb2db9-0b6d-491d-9529-d64e64e59014
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1905bc30afff4af0ffc74363b93f95732f4760f1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47631763"
---
# <a name="mixed-cursors"></a>Cursores mixtos
Un cursor mixto es una combinación de un cursor controlado por conjunto de claves y un cursor dinámico. Se usa cuando el conjunto de resultados es demasiado grande para razonablemente guardar las claves para el conjunto de resultados completo. Cursores mixtos se implementan mediante la creación de un conjunto de claves que es mayor que el conjunto de filas pero menor que el conjunto de resultados completo.  
  
 Siempre y cuando la aplicación se desplaza en el conjunto de claves, el comportamiento es controlado por conjunto de claves. Cuando la aplicación se desplaza fuera del conjunto de claves, el comportamiento es dinámico: el cursor recupera las filas solicitadas y crea un nuevo conjunto de claves. Una vez creado el nuevo conjunto de claves, el comportamiento se vuelve a cursores controlados por dentro de ese conjunto de claves.  
  
 Por ejemplo, suponga que un conjunto de resultados tiene 1.000 filas y utiliza un cursor mixto con un tamaño de conjunto de claves de 100 y un tamaño de conjunto de filas de 10. Cuando se captura el primer conjunto de filas, el cursor crea un conjunto de claves que consta de las claves de las 100 primeras filas. A continuación, devuelve las 10 primeras filas, como se solicitó.  
  
 Ahora suponga que otra aplicación elimina las filas 11 y 101. Si el cursor intenta recuperar la fila 11, producirá un "agujero" porque tiene una clave para esta fila, pero no hay ninguna fila; Esto es controlado por comportamiento. Si el cursor se intenta recuperar la fila 101, el cursor no detectará que falta la fila porque no tiene una clave para la fila. En su lugar, se recuperarán que anteriormente era fila 102. Este es el comportamiento de cursor dinámico.  
  
 Un cursor mixto es equivalente a un cursor dinámico cuando el tamaño del conjunto de claves es igual que el tamaño del conjunto de resultados. Un cursor mixto es equivalente a un cursor dinámico cuando el tamaño del conjunto de claves es igual a 1.
