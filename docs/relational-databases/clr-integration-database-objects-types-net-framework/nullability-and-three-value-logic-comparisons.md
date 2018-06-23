---
title: Nulabilidad y comparaciones lógicas de tres valores | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: reference
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- precision [CLR integration]
- overflow detections [CLR integration]
- null values [CLR integration]
- three-value logic comparisons [CLR integration]
- data types [CLR integration]
- SqlBoolean data type
ms.assetid: 13da4c7f-1010-4b2d-a63c-c69b6bfd96f1
caps.latest.revision: 38
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: cf097cfd86b5226f30658799a5c4eb1dd82ba053
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2018
ms.locfileid: "35700766"
---
# <a name="nullability-and-three-value-logic-comparisons"></a>Nulabilidad y comparaciones lógicas de tres valores
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Si está familiarizado con la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos, encontrará similar semántica y precisión en la **System.Data.SqlTypes** espacio de nombres en el [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]. No obstante, existen algunas diferencias, y en este tema se describen las más importantes.  
  
## <a name="null-values"></a>Valores NULL  
 Una de las diferencias principales que existen entre los tipos de datos nativos de Common Language Runtime (CLR) y los tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es que los primeros no permiten valores NULL, mientras que los últimos proporcionan una semántica completa de valores NULL.  
  
 Los valores NULL afectan a las comparaciones. Al comparar dos valores x e y, si alguno de los dos es NULL, hay una serie de comparaciones lógicas que se evalúan como un valor UNKNOWN en lugar de como True o False.  
  
## <a name="sqlboolean-data-type"></a>Tipo de datos SqlBoolean  
 El **System.Data.SqlTypes** espacio de nombres presenta un **SqlBoolean** tipo para representar esta lógica de 3 valores. Las comparaciones entre **SqlTypes** devolver un **SqlBoolean** tipo de valor. El valor UNKNOWN se representa mediante un valor null de la **SqlBoolean** tipo. Las propiedades **IsTrue**, **IsFalse**, y **IsNull** sirven para comprobar el valor de un **SqlBoolean** tipo.  
  
## <a name="operations-functions-and-null-values"></a>Operaciones, funciones y valores NULL  
 Todos los operadores aritméticos (+, -, \*, /, %), operadores bit a bit (~ &, y |), y la mayoría de las funciones devuelve NULL si alguno de los operandos o argumentos de **SqlTypes** son NULL. El **IsNull** propiedad siempre devuelve un valor true o false.  
  
## <a name="precision"></a>Precisión  
 Los tipos de datos decimales de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR tienen distintos valores máximos que los de los tipos de datos numéricos y decimales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Además, en [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR, los tipos de datos decimales asumen la precisión máxima. En el CLR para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], sin embargo, **SqlDecimal** proporciona la misma precisión máxima y escala y la misma semántica que el tipo de datos decimal en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="overflow-detection"></a>Detección de desbordamiento  
 En [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] CLR, la suma de dos números muy grandes no puede iniciar una excepción. En lugar de ello, si no se ha utilizado ningún operador de comprobación, el resultado devuelto puede "ajustarse" como un número entero negativo. En **System.Data.SqlTypes**, las excepciones se producen para todos los desbordamiento y subdesbordamiento errores y errores de división por cero.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos de SQL Server en .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
