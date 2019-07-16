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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085522"
---
# <a name="insert-statement-limitations"></a>Limitaciones de la instrucción de INSERCIÓN
Los datos insertados se truncan a la derecha sin previo aviso si es demasiado largo para caber en la columna.  
  
 Al intentar insertar un valor que está fuera del intervalo del tipo de datos de una columna hace que un valor NULL para insertarse en la columna.  
  
 Cuando se usa un archivo dBASE, Microsoft Excel, Paradox o Textdriver, insertar una cadena de longitud cero en una columna realmente inserta un valor NULL en su lugar.  
  
 Cuando se utiliza el controlador de Microsoft Excel, si se inserta una cadena vacía en una columna, una cadena vacía se convierte en un valor NULL; una instrucción SELECT de búsqueda que se ejecuta con una cadena vacía en la cláusula WHERE no surtirán efecto en esa columna.  
  
 Una tabla no es actualizable por el controlador de Paradox bajo dos condiciones:  
  
-   Cuando un índice único no se define en la tabla. Esto no es cierto para una tabla vacía, que se puede actualizar con una sola fila, incluso si no está definido un índice único en la tabla. Si se inserta una fila única en una tabla vacía que no tiene un índice único, una aplicación no se puede crear un índice único o insertar datos adicionales después de insertar la fila única.  
  
-   Si no se implementa el motor de base de datos de Borland, solo lectura y anexar instrucciones se permiten en la tabla de Paradox.  
  
 Cuando se usa el controlador de texto, valores NULL se representan mediante una cadena rellenada con caracteres de espacio en blanco en los archivos de longitud fija, pero se representan mediante sin espacios en blanco en archivos delimitados. Por ejemplo, en la siguiente fila que contiene tres campos, el segundo campo es un valor NULL:  
  
```  
"Smith:,, 123  
```  
  
 Cuando se usa el controlador de texto, todos los valores de columna pueden estar rellena con espacios iniciales. La longitud de cualquier fila debe ser menor o igual a 65,543 bytes.
