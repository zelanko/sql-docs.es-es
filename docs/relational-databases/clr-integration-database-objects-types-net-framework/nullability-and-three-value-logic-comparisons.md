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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68081318"
---
# <a name="nullability-and-three-value-logic-comparisons"></a>Nulabilidad y comparaciones lógicas de tres valores
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Si está familiarizado con el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos, encontrará similar semántica y precisión en la **System.Data.SqlTypes** espacio de nombres en el [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. No obstante, existen algunas diferencias, y en este tema se describen las más importantes.  
  
## <a name="null-values"></a>Valores NULL  
 Una de las diferencias principales que existen entre los tipos de datos nativos de Common Language Runtime (CLR) y los tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es que los primeros no permiten valores NULL, mientras que los últimos proporcionan una semántica completa de valores NULL.  
  
 Los valores NULL afectan a las comparaciones. Al comparar dos valores x e y, si alguno de los dos es NULL, hay una serie de comparaciones lógicas que se evalúan como un valor UNKNOWN en lugar de como True o False.  
  
## <a name="sqlboolean-data-type"></a>Tipo de datos SqlBoolean  
 El **System.Data.SqlTypes** introduce el espacio de nombres una **SqlBoolean** tipo para representar esta lógica de 3 valores. Las comparaciones entre **SqlTypes** devolver un **SqlBoolean** tipo de valor. El valor UNKNOWN se representa mediante un valor null de la **SqlBoolean** tipo. Las propiedades **IsTrue**, **IsFalse**, y **IsNull** sirven para comprobar el valor de un **SqlBoolean** tipo.  
  
## <a name="operations-functions-and-null-values"></a>Operaciones, funciones y valores NULL  
 Todos los operadores aritméticos (+, -, \*, /, %), operadores bit a bit (~ &, y |), y la mayoría de las funciones devuelve NULL si alguno de los operandos o argumentos de **SqlTypes** son NULL. El **IsNull** propiedad siempre devuelve un valor true o false.  
  
## <a name="precision"></a>Precisión  
 Los tipos de datos decimales de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR tienen distintos valores máximos que los de los tipos de datos numéricos y decimales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Además, en [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR, los tipos de datos decimales asumen la precisión máxima. En el CLR para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], sin embargo, **SqlDecimal** proporciona la misma precisión máxima y el escalado y la misma semántica que el tipo de datos decimal en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="overflow-detection"></a>Detección de desbordamiento  
 En [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR, la suma de dos números muy grandes no puede iniciar una excepción. En lugar de ello, si no se ha utilizado ningún operador de comprobación, el resultado devuelto puede "ajustarse" como un número entero negativo. En **System.Data.SqlTypes**, se inician excepciones para todos los desbordamiento y subdesbordamiento errores y errores de división por cero.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos de SQL Server en .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
