---
title: Tipos de datos de parámetro | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.reviewer: ''
manager: craigg
ms.openlocfilehash: e1f1097927f61355cf4a50f4287397d823fd3177
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56020123"
---
# <a name="parameter-data-types"></a>Tipos de datos de parámetro
Aunque cada parámetro especificado con **SQLBindParameter** se definen mediante un tipo de datos SQL, los parámetros en una instrucción SQL tener ningún intrínsecos tipo de datos. Por lo tanto, los marcadores de parámetros pueden incluirse en una instrucción SQL sólo si sus tipos de datos se pueden inferir de otro operando en la instrucción. ¿Por ejemplo, en una expresión aritmética, como? + COLUMN1, el tipo de datos del parámetro se puede inferir el tipo de datos de la columna con nombre representado por COLUMN1. Una aplicación no puede usar un marcador de parámetro si no se puede determinar el tipo de datos.  
  
 En la tabla siguiente se describe cómo se determina un tipo de datos para varios tipos de parámetros, de acuerdo con SQL-92. Para una especificación más completa de deducir el tipo de parámetro cuando se usan otras cláusulas SQL, vea la especificación de SQL-92.  
  
|Ubicación del parámetro|Supone que el tipo de datos|  
|---------------------------|-----------------------|  
|Un operando de un operador binario aritméticas o de comparación|Igual que el otro operando|  
|El primer operando de un **BETWEEN** cláusula|Igual que el segundo operando|  
|El segundo o tercer operando en un **BETWEEN** cláusula|Igual que el primer operando|  
|Una expresión que se utiliza con **IN**|Igual que el primer valor o la columna de resultados de la subconsulta|  
|Un valor que se utiliza con **IN**|Igual que la expresión o el primer valor si hay un marcador de parámetro en la expresión|  
|Un valor de patrón utilizado con **como**|VARCHAR|  
|Puede usar con un valor de actualización **actualizar**|Igual que la columna de actualización|
