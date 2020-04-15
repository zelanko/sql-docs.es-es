---
title: Cursores Mixtos (Mixed Cursors) Microsoft Docs
ms.custom: ''
ms.date: 01/20/2017
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a91dacf8ea9c0ed0db2c3b64634ddd53b854a534
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307440"
---
# <a name="mixed-cursors"></a>Cursores mixtos

Un cursor mixto es una combinación de un cursor controlado por conjunto de claves y un cursor dinámico. Se utiliza cuando el conjunto de resultados es demasiado grande para guardar razonablemente las claves para todo el conjunto de resultados. Los cursores mixtos se implementan mediante la creación de un conjunto de claves que es más pequeño que todo el conjunto de resultados, pero mayor que el conjunto de filas.  
  
 Siempre que la aplicación se desplace dentro del conjunto de claves, el comportamiento está controlado por conjuntos de claves. Cuando la aplicación se desplaza fuera del conjunto de claves, el comportamiento es dinámico: el cursor recupera las filas solicitadas y crea un nuevo conjunto de claves. Después de crear el nuevo conjunto de claves, el comportamiento vuelve a ser controlado por el conjunto de claves dentro de ese conjunto de claves.  
  
 Por ejemplo, supongamos que un conjunto de resultados tiene 1.000 filas y utiliza un cursor mixto con un tamaño de conjunto de claves de 100 y un tamaño de conjunto de filas de 10. Cuando se captura el primer conjunto de filas, el cursor crea un conjunto de claves que consta de las claves de las primeras 100 filas. A continuación, devuelve las primeras 10 filas, según se solicita.  
  
 Ahora supongamos que otra aplicación elimina las filas 11 y 101. Si el cursor intenta recuperar la fila 11, se encontrará con un espacio porque tiene una clave para esta fila, pero no existe ninguna fila; este es un comportamiento basado en conjuntos de claves. Si el cursor intenta recuperar la fila 101, el cursor no detectará que falta la fila porque no tiene una clave para la fila. En su lugar, recuperará lo que anteriormente era la fila 102. Este es el comportamiento dinámico del cursor.  
  
 Un cursor mixto es equivalente a un cursor controlado por conjunto de claves cuando el tamaño del conjunto de claves es igual al tamaño del conjunto de resultados. Un cursor mixto equivale a un cursor dinámico cuando el tamaño del conjunto de claves es igual a 1.
