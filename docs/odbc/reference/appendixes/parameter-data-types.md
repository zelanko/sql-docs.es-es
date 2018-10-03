---
title: Tipos de datos de parámetro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
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
manager: craigg
ms.openlocfilehash: e6c2a73aec119b7572cad93dedb2994235329cb2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47826036"
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
