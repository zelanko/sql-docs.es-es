---
title: Nulabilidad y comparaciones lógicas de tres valores | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- precision [CLR integration]
- overflow detections [CLR integration]
- null values [CLR integration]
- three-value logic comparisons [CLR integration]
- data types [CLR integration]
- SqlBoolean data type
ms.assetid: 13da4c7f-1010-4b2d-a63c-c69b6bfd96f1
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4f1b4823db4ae961024ac2a786c948d8349f31be
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62919637"
---
# <a name="nullability-and-three-value-logic-comparisons"></a>Nulabilidad y comparaciones lógicas de tres valores
  Si está familiarizado con los tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], observará una semántica y precisión similares en el espacio de nombres `System.Data.SqlTypes` de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. No obstante, existen algunas diferencias, y en este tema se describen las más importantes.  
  
## <a name="null-values"></a>Valores NULL  
 Una de las diferencias principales que existen entre los tipos de datos nativos de Common Language Runtime (CLR) y los tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es que los primeros no permiten valores NULL, mientras que los últimos proporcionan una semántica completa de valores NULL.  
  
 Los valores NULL afectan a las comparaciones. Al comparar dos valores x e y, si alguno de los dos es NULL, hay una serie de comparaciones lógicas que se evalúan como un valor UNKNOWN en lugar de como True o False.  
  
## <a name="sqlboolean-data-type"></a>Tipo de datos SqlBoolean  
 El espacio de nombres `System.Data.SqlTypes` introduce un tipo `SqlBoolean` para representar esta lógica de 3 valores. Las comparaciones entre `SqlTypes` devuelven un tipo de valor `SqlBoolean`. El valor UNKNOWN se representa mediante un valor NULL de tipo `SqlBoolean`. Las propiedades `IsTrue`, `IsFalse` e `IsNull` se proporcionan para comprobar el valor de un tipo `SqlBoolean`.  
  
## <a name="operations-functions-and-null-values"></a>Operaciones, funciones y valores NULL  
 Todos los operadores aritméticos (+, -, \*, /, %), operadores bit a bit (~ &, y |), y la mayoría de las funciones devuelve NULL si alguno de los operandos o argumentos de `SqlTypes` son NULL. La propiedad `IsNull` siempre devuelve un valor True o False.  
  
## <a name="precision"></a>Precisión  
 Los tipos de datos decimales de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR tienen distintos valores máximos que los de los tipos de datos numéricos y decimales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Además, en [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR, los tipos de datos decimales asumen la precisión máxima. Sin embargo, en CLR para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], `SqlDecimal` proporciona la misma precisión máxima, la misma escala máxima y la misma semántica que el tipo de datos decimal de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="overflow-detection"></a>Detección de desbordamiento  
 En [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR, la suma de dos números muy grandes no puede iniciar una excepción. En lugar de ello, si no se ha utilizado ningún operador de comprobación, el resultado devuelto puede "ajustarse" como un número entero negativo. En `System.Data.SqlTypes`, se inician excepciones para todos los errores de desbordamiento, subdesbordamiento y división por cero.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos de SQL Server en .NET Framework](sql-server-data-types-in-the-net-framework.md)  
  
  
