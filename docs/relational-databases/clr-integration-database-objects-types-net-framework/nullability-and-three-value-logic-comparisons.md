---
title: Nulabilidad y comparaciones lógicas de tres valores | Microsoft Docs
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
ms.openlocfilehash: e5dbdf757038abbf2c98d3987ee14a9cb9184a61
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68081318"
---
# <a name="nullability-and-three-value-logic-comparisons"></a>Nulabilidad y comparaciones lógicas de tres valores
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Si está familiarizado con los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos, encontrará una semántica y una precisión similares en el espacio de nombres **System. Data. SqlTypes** en [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. No obstante, existen algunas diferencias, y en este tema se describen las más importantes.  
  
## <a name="null-values"></a>Valores NULL  
 Una de las diferencias principales que existen entre los tipos de datos nativos de Common Language Runtime (CLR) y los tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es que los primeros no permiten valores NULL, mientras que los últimos proporcionan una semántica completa de valores NULL.  
  
 Los valores NULL afectan a las comparaciones. Al comparar dos valores x e y, si alguno de los dos es NULL, hay una serie de comparaciones lógicas que se evalúan como un valor UNKNOWN en lugar de como True o False.  
  
## <a name="sqlboolean-data-type"></a>Tipo de datos SqlBoolean  
 El espacio de nombres **System. Data. SqlTypes** introduce un tipo **SqlBoolean** para representar esta lógica de 3 valores. Las comparaciones entre los **SqlTypes** devuelven un tipo de valor de **SqlBoolean** . El valor desconocido se representa mediante el valor null del tipo **SqlBoolean** . Se proporcionan las propiedades **IsTrue**, **IsFalse**e **IsNull** para comprobar el valor de un tipo **SqlBoolean** .  
  
## <a name="operations-functions-and-null-values"></a>Operaciones, funciones y valores NULL  
 Todos los operadores aritméticos (+, \*-,,/,%), los operadores bit a bit (~, & y |) y la mayoría de las funciones devuelven NULL si alguno de los operandos o argumentos de **SqlTypes** es NULL. La propiedad **IsNull** siempre devuelve un valor true o false.  
  
## <a name="precision"></a>Precision  
 Los tipos de datos decimales de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR tienen distintos valores máximos que los de los tipos de datos numéricos y decimales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Además, en [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR, los tipos de datos decimales asumen la precisión máxima. En el CLR de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], sin embargo, **SqlDecimal** proporciona la misma precisión y escala máximas, y la misma semántica que el tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]decimal de.  
  
## <a name="overflow-detection"></a>Detección de desbordamiento  
 En [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR, la suma de dos números muy grandes no puede iniciar una excepción. En lugar de ello, si no se ha utilizado ningún operador de comprobación, el resultado devuelto puede "ajustarse" como un número entero negativo. En **System. Data. SqlTypes**, se producen excepciones para todos los errores de desbordamiento y subdesbordamiento, y los errores de división por cero.  
  
## <a name="see-also"></a>Consulte también  
 [Tipos de datos de SQL Server en .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
