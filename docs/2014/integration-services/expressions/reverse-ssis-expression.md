---
title: REVERSE (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- REVERSE function
- reverse character expressions
ms.assetid: bcebcc55-7247-4896-8f53-4d582d58cfb4
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 02175d277793a1be7ca7d82edc4fd47b862d26f3
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199401"
---
# <a name="reverse-ssis-expression"></a>REVERSE (expresión de SSIS)
  Devuelve una expresión de caracteres en orden inverso.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
REVERSE(character_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 Expresión de caracteres que se va a invertir.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_WSTR  
  
## <a name="remarks"></a>Notas  
 El argumento *character_expression* ha de tener el tipo de datos DT_WSTR.  
  
 REVERSE devuelve un resultado NULL si el valor de *character_expression* es NULL.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo usa un literal de cadena. El resultado devuelto es "ekiB niatnuoM".  
  
```  
REVERSE("Mountain Bike")  
```  
  
 En este ejemplo se utiliza una variable. Si **Name** contiene Touring Bike, el resultado devuelto es "ekiB gniruoT".  
  
```  
REVERSE(@Name)  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones &#40;expresión de SSIS&#41;](functions-ssis-expression.md)  
  
  