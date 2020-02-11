---
title: Limitaciones de la instrucción INSERT | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1676af6216ac703e9a8976951ec2888b9e940b67
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68085522"
---
# <a name="insert-statement-limitations"></a>Limitaciones de la instrucción de INSERCIÓN
Los datos insertados se truncan a la derecha sin previo aviso si es demasiado largo para caber en la columna.  
  
 Al intentar insertar un valor que está fuera del intervalo del tipo de datos de una columna, se inserta un valor NULL en la columna.  
  
 Cuando se usa dBASE, Microsoft Excel, Paradox o Textdriver, al insertar una cadena de longitud cero en una columna se inserta realmente un valor NULL.  
  
 Cuando se utiliza el controlador de Microsoft Excel, si se inserta una cadena vacía en una columna, la cadena vacía se convierte en un valor NULL. una instrucción SELECT de búsqueda que se ejecuta con una cadena vacía en la cláusula WHERE no se realizará correctamente en esa columna.  
  
 Una tabla no es actualizable por el controlador de Paradox en dos condiciones:  
  
-   Cuando no se define un índice único en la tabla. Esto no es cierto para una tabla vacía, que se puede actualizar con una sola fila aunque no se haya definido un índice único en la tabla. Si se inserta una sola fila en una tabla vacía que no tiene un índice único, una aplicación no puede crear un índice único o insertar datos adicionales después de que se haya insertado la fila única.  
  
-   Si no se implementa Borland Motor de base de datos, solo se permiten las instrucciones Read y Append en la tabla de Paradox.  
  
 Cuando se usa el controlador de texto, los valores NULL se representan mediante una cadena rellenada en blanco en archivos de longitud fija, pero se representan sin espacios en los archivos delimitados. Por ejemplo, en la siguiente fila que contiene tres campos, el segundo campo es un valor nulo:  
  
```  
"Smith:,, 123  
```  
  
 Cuando se usa el controlador de texto, todos los valores de columna se pueden rellenar con espacios iniciales. La longitud de cualquier fila debe ser menor o igual que 65.543 bytes.
