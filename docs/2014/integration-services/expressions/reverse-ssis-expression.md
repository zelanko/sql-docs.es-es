---
title: REVERSE (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- REVERSE function
- reverse character expressions
ms.assetid: bcebcc55-7247-4896-8f53-4d582d58cfb4
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e28592369427d480fc46eb8d7e8801272a7554a2
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52801737"
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
  
## <a name="remarks"></a>Comentarios  
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
  
  
