---
title: ISNULL (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- null values [Integration Services]
- ISNULL function
ms.assetid: 88dbf49e-1307-4dda-b9db-ff1632053550
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 3f654539eb4fbef89b0882b7996b59474c11e1be
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68080723"
---
# <a name="isnull-ssis-expression"></a>ISNULL (expresión de SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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
  
## <a name="see-also"></a>Consulte también  
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)   
 [COALESCE &#40;Transact-SQL&#41;](../../t-sql/language-elements/coalesce-transact-sql.md)  
  
  
