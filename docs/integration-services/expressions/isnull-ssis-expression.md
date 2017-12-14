---
title: "ISNULL (expresión de SSIS) | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- null values [Integration Services]
- ISNULL function
ms.assetid: 88dbf49e-1307-4dda-b9db-ff1632053550
caps.latest.revision: "28"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e6ea60ae5d0c417b228619a3e177c3b9d0777369
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
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
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)   
 [COALESCE &#40;Transact-SQL&#41;](../../t-sql/language-elements/coalesce-transact-sql.md)  
  
  
