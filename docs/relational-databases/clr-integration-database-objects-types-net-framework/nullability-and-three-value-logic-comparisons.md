---
title: Comparaciones de nulidad y lógica de tres valores Microsoft Docs
description: En este artículo se explica cómo los tipos de datos de SQL ServerSQL Server difieren de los tipos de System.Data.SqlTypes en .NET Framework, que tienen una semántica y precisión similares.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
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
ms.openlocfilehash: 3f016abf2113afef3e02f01fd9842b91b742d50a
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488480"
---
# <a name="nullability-and-three-value-logic-comparisons"></a>Nulabilidad y comparaciones lógicas de tres valores
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Si está familiarizado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con los tipos de datos, encontrará una semántica y precisión similares en el espacio de nombres **System.Data.SqlTypes** del [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]archivo . No obstante, existen algunas diferencias, y en este tema se describen las más importantes.  
  
## <a name="null-values"></a>Valores NULL  
 Una de las diferencias principales que existen entre los tipos de datos nativos de Common Language Runtime (CLR) y los tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es que los primeros no permiten valores NULL, mientras que los últimos proporcionan una semántica completa de valores NULL.  
  
 Los valores NULL afectan a las comparaciones. Al comparar dos valores x e y, si alguno de los dos es NULL, hay una serie de comparaciones lógicas que se evalúan como un valor UNKNOWN en lugar de como True o False.  
  
## <a name="sqlboolean-data-type"></a>Tipo de datos SqlBoolean  
 El espacio de nombres **System.Data.SqlTypes** introduce un tipo **SqlBoolean** para representar esta lógica de 3 valores. Las comparaciones entre **cualquier SqlTypes** devuelven un **SqlBoolean** tipo de valor. El unknown valor se representa mediante el valor nulo de la **SqlBoolean** tipo. Las propiedades **IsTrue**, **IsFalse**y **IsNull** se proporcionan para comprobar el valor de un **SqlBoolean** tipo.  
  
## <a name="operations-functions-and-null-values"></a>Operaciones, funciones y valores NULL  
 Todos los operadores aritméticos (+, -, \*, , /, %), los operadores bit a bit (en & y ) y la mayoría de las funciones devuelven NULL si alguno de los operandos o argumentos de **SqlTypes** son NULL. El **IsNull** propiedad siempre devuelve un valor true o false.  
  
## <a name="precision"></a>Precision  
 Los tipos de datos decimales de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR tienen distintos valores máximos que los de los tipos de datos numéricos y decimales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Además, en [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR, los tipos de datos decimales asumen la precisión máxima. En el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]CLR para , sin embargo, **SqlDecimal** proporciona la misma precisión y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]escala máxima, y la misma semántica que el tipo de datos decimales en .  
  
## <a name="overflow-detection"></a>Detección de desbordamiento  
 En [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR, la suma de dos números muy grandes no puede iniciar una excepción. En lugar de ello, si no se ha utilizado ningún operador de comprobación, el resultado devuelto puede "ajustarse" como un número entero negativo. En **System.Data.SqlTypes**, se producen excepciones para todos los errores de desbordamiento y subdesbordamiento y errores de división por cero.  
  
## <a name="see-also"></a>Consulte también  
 [Tipos de datos de SQL Server en .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
