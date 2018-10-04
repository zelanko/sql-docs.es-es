---
title: ISNULL (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- null values [Integration Services]
- ISNULL function
ms.assetid: 88dbf49e-1307-4dda-b9db-ff1632053550
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6780ed81142343e0e08ff624ee80e8ef2cc532c8
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48129825"
---
# <a name="isnull-ssis-expression"></a>ISNULL (expresión de SSIS)
  Devuelve un resultado booleano en función de si una expresión es NULL.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
ISNULL(expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression*  
 Expresión válida de cualquier tipo de datos.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_BOOL  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo devuelve TRUE si la columna **DiscontinuedDate** contiene un valor NULL.  
  
```  
ISNULL(DiscontinuedDate)  
```  
  
 Este ejemplo devuelve "Unknown last name" si el valor de la columna **LastName** es NULL; en caso contrario, devuelve el valor de **LastName**.  
  
```  
ISNULL(LastName)? "Unknown last name":LastName  
```  
  
 Este ejemplo siempre devuelve TRUE si la columna **DaysToManufacture** es NULL, independientemente del valor de la variable **AddDays**.  
  
```  
ISNULL(DaysToManufacture + @AddDays)  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones &#40;expresión de SSIS&#41;](functions-ssis-expression.md)   
 [COALESCE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/coalesce-transact-sql)  
  
  
