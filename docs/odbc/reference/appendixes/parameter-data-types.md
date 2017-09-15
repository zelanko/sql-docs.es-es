---
title: "Tipos de datos de parámetro | Documentos de Microsoft"
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
- data types [ODBC], parameters
- parameter data type [ODBC]
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: fd7e99d8-d26a-408c-9733-6ffccde99f75
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5dcd41f599a6e57a55d05a8a869363ec70c5f756
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="parameter-data-types"></a>Tipos de datos de parámetro
Aunque cada parámetro especificado con **SQLBindParameter** se definen mediante un tipo de datos SQL, los parámetros en una instrucción SQL tener ningún intrínsecos tipo de datos. Por lo tanto, los marcadores de parámetros pueden incluirse en una instrucción SQL solo si se pueden inferir a sus tipos de datos desde el otro operando de la instrucción. ¿Por ejemplo, en una expresión aritmética, como? + COLUMN1, el tipo de datos del parámetro se puede inferir el tipo de datos de la columna con nombre representado por COLUMN1. Una aplicación no puede utilizar un marcador de parámetro si no se puede determinar el tipo de datos.  
  
 En la tabla siguiente describe cómo se determina un tipo de datos para varios tipos de parámetros, con arreglo a SQL-92. Para una especificación más completa en deducir el tipo de parámetro cuando se usan otras cláusulas SQL, vea la especificación de SQL-92.  
  
|Ubicación del parámetro|Supone que el tipo de datos|  
|---------------------------|-----------------------|  
|Un operando de un operador aritmético o de comparación binario|Igual que el otro operando|  
|El primer operando de un **BETWEEN** cláusula|Igual que el segundo operando|  
|El segundo o tercer operando en una **BETWEEN** cláusula|Igual que el primer operando|  
|Una expresión que se utiliza con **en**|Igual que el primer valor o la columna de resultados de la subconsulta|  
|Un valor que se utiliza con **en**|Igual que la expresión o el primer valor si hay un marcador de parámetro en la expresión|  
|Un valor de patrón que se utiliza con **como**|VARCHAR|  
|Un valor de actualización que se utiliza con **actualizar**|Igual que la columna de actualización|
