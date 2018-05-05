---
title: (División) (DMX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- / (divide)
- divide operator (/)
ms.assetid: 7afc06cd-054b-48c3-9c3c-9a0c17d15e63
caps.latest.revision: 14
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 00e4712dd44860c673f67d62d7eb1d6ff0bd5d5c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="divide-dmx"></a>(División) (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Realiza una operación aritmética que divide un número por otro número.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Dividend / Divisor  
```  
  
#### <a name="parameters"></a>Parámetros  
 *dividendo*  
 Expresión DMX (Extensiones de minería de datos) válida que devuelve un valor numérico.  
  
 *divisor*  
 Expresión DMX válida que devuelve un valor numérico.  
  
## <a name="return-value"></a>Valor devuelto  
 Valor cuyo tipo de datos es el del parámetro con la mayor precedencia.  
  
## <a name="remarks"></a>Comentarios  
 El valor que devuelve el operador es el cociente de la primera expresión dividida por la segunda expresión.  
  
 Ambas expresiones deben ser del mismo tipo de datos o una se debe poder convertir implícitamente en el tipo de datos de la otra. Si el divisor se evalúa como un valor NULL, el operador genera un error. Si tanto el divisor como el dividendo se evalúan como un valor NULL, el operador devuelve un valor NULL.  
  
## <a name="see-also"></a>Vea también  
 [Operadores aritméticos &#40;DMX&#41;](../dmx/operators-arithmetic.md)   
 [Extensiones de minería de datos &#40;DMX&#41; Referencia de operadores](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Operadores &#40;DMX&#41;](../dmx/operators-dmx.md)   
 [Dividir &#40;expresión de SSIS&#41;](../integration-services/expressions/divide-ssis-expression.md)   
 [&#40;Dividir&#41; &#40;Transact-SQL&#41;](../t-sql/language-elements/divide-transact-sql.md)  
  
  
