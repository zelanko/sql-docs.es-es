---
title: Limitaciones de la Declaración INSERT (INSERT Statement Limitations) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, INSERT statement limitations
- INSERT statement limitations [ODBC]
- truncation of data [ODBC]
ms.assetid: dea05698-527a-41ab-8729-bbed85556185
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f903f15ec13baa28a789891c1527dc742daa68ac
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300015"
---
# <a name="insert-statement-limitations"></a>Limitaciones de la instrucción de INSERCIÓN
Los datos insertados se truncan a la derecha sin previo aviso si es demasiado largo para caber en la columna.  
  
 Al intentar insertar un valor que está fuera del intervalo del tipo de datos de una columna, se inserta un valor NULL en la columna.  
  
 Cuando se usa un dBASE, Microsoft Excel, Paradox o Textdriver, insertar una cadena de longitud cero en una columna inserta realmente un NULL en su lugar.  
  
 Cuando se utiliza el controlador de Microsoft Excel, si se inserta una cadena vacía en una columna, la cadena vacía se convierte en NULL; una instrucción SELECT buscada que se ejecuta con una cadena vacía en la cláusula WHERE no se realizará correctamente en esa columna.  
  
 Una tabla no es actualizable por el controlador Paradox bajo dos condiciones:  
  
-   Cuando no se define un índice único en la tabla. Esto no es cierto para una tabla vacía, que se puede actualizar con una sola fila, incluso si no se define un índice único en la tabla. Si se inserta una sola fila en una tabla vacía que no tiene un índice único, una aplicación no puede crear un índice único ni insertar datos adicionales después de insertar la fila única.  
  
-   Si el Motor de base de datos de Borland no está implementado, solo se permiten instrucciones de lectura y anexión en la tabla Paradox.  
  
 Cuando se utiliza el controlador de texto, los valores NULL se representan mediante una cadena rellenada en blanco en archivos de longitud fija, pero no se representan mediante espacios en archivos delimitados. Por ejemplo, en la fila siguiente que contiene tres campos, el segundo campo es un valor NULL:  
  
```  
"Smith:,, 123  
```  
  
 Cuando se utiliza el controlador de texto, todos los valores de columna se pueden rellenar con espacios iniciales. La longitud de cualquier fila debe ser menor o igual que 65.543 bytes.
