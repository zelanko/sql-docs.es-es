---
title: Tipos de datos de parámetros ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], parameters
- parameter data type [ODBC]
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: fd7e99d8-d26a-408c-9733-6ffccde99f75
author: David-Engel
ms.author: v-daenge
ms.reviewer: ''
ms.openlocfilehash: f29bb70937df32e03480c13c7ef739eb273f15eb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303586"
---
# <a name="parameter-data-types"></a>Tipos de datos de parámetro
Aunque cada parámetro especificado con **SQLBindParameter** se define mediante un tipo de datos SQL, los parámetros de una instrucción SQL no tienen ningún tipo de datos intrínseco. Por lo tanto, los marcadores de parámetro se pueden incluir en una instrucción SQL solo si sus tipos de datos se pueden deducir de otro operando de la instrucción. Por ejemplo, en una expresión aritmética como ? + COLUMN1, el tipo de datos del parámetro se puede deducir del tipo de datos de la columna con nombre representada por COLUMN1. Una aplicación no puede utilizar un marcador de parámetro si no se puede determinar el tipo de datos.  
  
 En la tabla siguiente se describe cómo se determina un tipo de datos para varios tipos de parámetros, de acuerdo con SQL-92. Para obtener una especificación más completa sobre la inferir el tipo de parámetro cuando se utilizan otras cláusulas SQL, consulte la especificación SQL-92.  
  
|Ubicación del parámetro|Tipo de datos asumido|  
|---------------------------|-----------------------|  
|Un operando de un operador de comparación o aritmética binaria|Igual que el otro operando|  
|El primer operando de una cláusula **BETWEEN**|Igual que el segundo operando|  
|El segundo o tercer operando de una cláusula **BETWEEN**|Igual que el primer operando|  
|Expresión utilizada con **IN**|Igual que el primer valor o la columna de resultados de la subconsulta|  
|Un valor utilizado con **IN**|Igual que la expresión o el primer valor si hay un marcador de parámetro en la expresión|  
|Un valor de patrón utilizado con **LIKE**|VARCHAR|  
|Un valor de actualización utilizado con **UPDATE**|Igual que la columna de actualización|
